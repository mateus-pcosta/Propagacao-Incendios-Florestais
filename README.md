# Sistema Preditivo para Estimativa da Velocidade de Propagação de Incêndios Florestais

Repositório de coleta, processamento e integração de dados para o artigo. Os notebooks cobrem desde a aquisição das fontes brutas até a geração do dataset tabular final para modelagem.

## Estrutura

```
artigo_incendio/
├── 01_focos_calor.ipynb          # Focos de calor — INPE Queimadas (WFS) + NASA FIRMS VIIRS
├── 02_dados_meteorologicos.ipynb # Variáveis meteorológicas — ERA5 (CDS API) + INMET
├── 03_cobert_uso_solo.ipynb      # Cobertura e uso do solo — MapBiomas Col. 7 + PRODES
├── 04_relevo.ipynb               # Relevo e topografia — SRTM 30m via OpenTopoData
├── 05_meteo_por_foco.ipynb       # Condições meteorológicas ERA5 por foco (join espacial)
├── 06_velocidade_propagacao.ipynb# Estimativa de velocidade — DBSCAN + Haversine
├── 07_consolidacao_final.ipynb   # Integração de todas as fontes → dataset para modelagem
├── requirements.txt
├── README.md
└── data/                         # Gerado automaticamente ao rodar os notebooks
    ├── inpe_queimadas/            # CSVs mensais + consolidado INPE (189.901 focos)
    ├── firms/                     # CSVs FIRMS VIIRS (SNPP + NOAA-20)
    ├── era5/                      # NetCDF mensais ERA5 + CSV ERA5 por foco + figuras
    ├── inmet/                     # ZIP + CSVs das estações automáticas INMET
    ├── mapbiomas/                 # Raster MapBiomas (COG) + CSV focos × cobertura
    ├── prodes/                    # Série histórica desmatamento PRODES
    ├── relevo/                    # CSV altitudes SRTM + figuras
    ├── velocidade/                # CSV focos com evento_id e velocidade estimada
    └── dataset_final_2023.parquet # Saída final integrada (gerada pelo nb07)
```

> `data/` está no `.gitignore`. Os notebooks baixam os dados automaticamente na primeira execução — basta ter conexão com a internet.

## Pré-requisitos

```bash
pip install -r requirements.txt
```

> **ERA5:** crie `~/.cdsapirc` com suas credenciais do Copernicus CDS:
> ```
> url: https://cds.climate.copernicus.eu/api
> key: SEU_UID:SUA_API_KEY
> ```
> Cadastro e token pessoal em [cds.climate.copernicus.eu/profile](https://cds.climate.copernicus.eu/profile)
> — instruções completas em [cds.climate.copernicus.eu/how-to-api](https://cds.climate.copernicus.eu/how-to-api)

> **NASA FIRMS:** defina `FIRMS_KEY` no notebook 01 com sua chave da API.
> Cadastro gratuito em [firms.modaps.eosdis.nasa.gov](https://firms.modaps.eosdis.nasa.gov/api/)

## Como usar

Execute os notebooks em ordem. Cada um salva seus resultados em `data/` e os notebooks seguintes os leem como cache.

| Notebook | Entrada | Saída |
|---|---|---|
| `01_focos_calor` | — | `inpe_focos_2023_consolidado.csv` |
| `02_dados_meteorologicos` | — | `era5_2023_MM_brasil.nc` (×12) |
| `03_cobert_uso_solo` | focos (nb01) | `focos_mapbiomas_2023.csv` |
| `04_relevo` | focos (nb01) | `focos_altitude_completo_2023.csv` |
| `05_meteo_por_foco` | focos (nb01) + ERA5 (nb02) | `focos_era5_2023.csv` |
| `06_velocidade_propagacao` | focos (nb01) | `focos_velocidade_2023.csv` |
| `07_consolidacao_final` | saídas de todos | `dataset_final_2023.parquet` |

## Fontes de dados

| Notebook | Fonte | Acesso |
|---|---|---|
| `01` | INPE Queimadas — GeoServer WFS | Público, sem chave |
| `01` | NASA FIRMS VIIRS — API histórica | Chave gratuita ([FIRMS](https://firms.modaps.eosdis.nasa.gov/api/)) |
| `02` | ERA5 ECMWF — Copernicus CDS API | Conta gratuita ([CDS](https://cds.climate.copernicus.eu/)) |
| `02` | INMET Dados Históricos | Público, sem chave |
| `03` | MapBiomas Coleção 7 (COG/GCS) | Público, sem chave |
| `03` | PRODES/INPE — série histórica | Público, sem chave |
| `04` | SRTM 30m via OpenTopoData | Público, sem chave |
