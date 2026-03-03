# Sistema Preditivo para Estimativa da Velocidade de Propagação de Incêndios Florestais

Repositório de coleta e processamento de dados para o artigo.

## Estrutura

```
artigo_incendio/
├── 01_focos_calor.ipynb      # Focos de calor — INPE Queimadas (WFS)
├── README.md
└── data/                     # Gerado automaticamente ao rodar os notebooks
    └── inpe_queimadas/       # CSVs mensais baixados do GeoServer INPE
```

> `data/` está no `.gitignore`. Os notebooks baixam os dados automaticamente na primeira execução — basta ter conexão com a internet.

## Pré-requisitos

```bash
pip install pandas requests matplotlib urllib3
```

## Como usar

Execute os notebooks em ordem. Cada um baixa seus próprios dados ao ser rodado pela primeira vez e salva em cache local (`data/`).

## Fontes de dados

| Notebook | Fonte | Acesso |
|---|---|---|
| `01_focos_calor` | INPE Queimadas — GeoServer WFS | Público, sem chave |
| `02_era5` (em breve) | ERA5 ECMWF | Conta gratuita [Copernicus CDS](https://cds.climate.copernicus.eu/) |
| `03_mapbiomas` (em breve) | MapBiomas | Conta gratuita [GEE](https://earthengine.google.com/) |
| `04_srtm` (em breve) | SRTM NASA | Público |
