# Sistema Preditivo para Estimativa da Velocidade de Propagação de Incêndios Florestais

Repositório de coleta e processamento de dados para o artigo.

## Estrutura

```
artigo_incendio/
├── 01_focos_calor.ipynb          # Focos de calor — INPE Queimadas (WFS)
├── 02_dados_meteorologicos.ipynb # Variáveis meteorológicas — ERA5 (CDS API) + INMET
├── 03_cobert_uso_solo.ipynb      # Cobertura e uso do solo — MapBiomas Col. 7 + PRODES
├── 04_relevo.ipynb               # Relevo e topografia — SRTM 30m via OpenTopoData
├── README.md
└── data/                         # Gerado automaticamente ao rodar os notebooks
    ├── inpe_queimadas/            # CSVs mensais + consolidado INPE
    ├── era5/                      # NetCDF mensais ERA5 + CSV diário + figuras
    ├── inmet/                     # ZIP + CSVs das estações automáticas INMET
    ├── mapbiomas/                 # Raster MapBiomas (COG) + CSV focos × cobertura
    ├── prodes/                    # Série histórica desmatamento PRODES
    └── relevo/                    # CSV altitudes SRTM + figuras
```

> `data/` está no `.gitignore`. Os notebooks baixam os dados automaticamente na primeira execução — basta ter conexão com a internet.

## Pré-requisitos

```bash
pip install pandas requests matplotlib urllib3 xarray netCDF4 cdsapi numpy rasterio
```

> **ERA5:** crie `~/.cdsapirc` com suas credenciais do Copernicus CDS:
> ```
> url: https://cds.climate.copernicus.eu/api/v2
> key: SEU_UID:SUA_API_KEY
> ```
> Cadastro gratuito em [cds.climate.copernicus.eu](https://cds.climate.copernicus.eu/user/register)

## Como usar

Execute os notebooks em ordem. Cada um baixa seus próprios dados ao ser rodado pela primeira vez e salva em cache local (`data/`). O notebook 04 depende do CSV de focos gerado pelo 01 e, opcionalmente, dos CSVs dos notebooks 02 e 03.

## Fontes de dados

| Notebook | Fonte | Acesso |
|---|---|---|
| `01_focos_calor` | INPE Queimadas — GeoServer WFS | Público, sem chave |
| `02_dados_meteorologicos` | ERA5 ECMWF + INMET Dados Históricos | ERA5: conta gratuita [Copernicus CDS](https://cds.climate.copernicus.eu/) · INMET: público |
| `03_cobert_uso_solo` | MapBiomas Coleção 7 (COG/GCS) + PRODES/INPE | Público, sem chave |
| `04_relevo` | SRTM 30m via [OpenTopoData](https://www.opentopodata.org/) | Público, sem chave |
