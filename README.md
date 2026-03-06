# Sistema Preditivo para Estimativa da Velocidade de Propagação de Incêndios Florestais

Repositório de coleta e processamento de dados para o artigo.

## Estrutura

```
artigo_incendio/
├── 01_focos_calor.ipynb         # Focos de calor — INPE Queimadas (WFS)
├── 02_dados_meteorologicos.ipynb # Variáveis meteorológicas — ERA5 (CDS API) + INMET
├── README.md
└── data/                        # Gerado automaticamente ao rodar os notebooks
    ├── inpe_queimadas/           # CSVs mensais baixados do GeoServer INPE
    ├── era5/                     # NetCDF mensais ERA5 + figuras geradas
    └── inmet/                    # ZIP + CSVs das estações automáticas INMET
```

> `data/` está no `.gitignore`. Os notebooks baixam os dados automaticamente na primeira execução — basta ter conexão com a internet.

## Pré-requisitos

```bash
pip install pandas requests matplotlib urllib3 xarray netCDF4 cdsapi numpy
```

> **ERA5:** crie `~/.cdsapirc` com suas credenciais do Copernicus CDS:
> ```
> url: https://cds.climate.copernicus.eu/api/v2
> key: SEU_UID:SUA_API_KEY
> ```
> Cadastro gratuito em [cds.climate.copernicus.eu](https://cds.climate.copernicus.eu/user/register)

## Como usar

Execute os notebooks em ordem. Cada um baixa seus próprios dados ao ser rodado pela primeira vez e salva em cache local (`data/`).

## Fontes de dados

| Notebook | Fonte | Acesso |
|---|---|---|
| `01_focos_calor` | INPE Queimadas — GeoServer WFS | Público, sem chave |
| `02_dados_meteorologicos` | ERA5 ECMWF + INMET Dados Históricos | ERA5: conta gratuita [Copernicus CDS](https://cds.climate.copernicus.eu/) · INMET: público |
| `03_mapbiomas` (em breve) | MapBiomas | Conta gratuita [GEE](https://earthengine.google.com/) |
| `04_srtm` (em breve) | SRTM NASA | Público |
