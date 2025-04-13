# NDVI Prediction 

Este repositório contém um pipeline completo para a previsão do Índice de Vegetação por Diferença Normalizada (NDVI) utilizando dados de satélite Sentinel-1, Sentinel-2. O objetivo principal é gerar previsões de NDVI e compará-las com valores reais para análise e tomada de decisão.

## Por que usar o NDVI Prediction ?



## Fluxograma do projeto



## Estrutura do Repositório
### **Step One: Carregamento e Download de Dados**
1. **Carregar Pontos no Banco de Dados**: Os pontos de interesse são carregados no banco de dados PostgreSQL.
2. **Download de Dados Sentinel**: Utiliza a API do Google Earth Engine (GEE) para baixar dados do Sentinel-1 e Sentinel-2.
3. **Download de Dados Climáticos**: Obtém variáveis climáticas (temperatura, precipitação, etc.) do repositório ERA5.

### **Step Two: Treinamento do Modelo**
1. **Análise Exploratória**: Identificação de outliers e análise de distribuição dos dados.
2. **Treinamento do Modelo**: Um modelo de regressão polinomial é treinado para prever o NDVI com base em variáveis como `cr_s1`, `ndvi_s2_moving_avg` e o dia juliano.

### **Step Three: Previsão e Geração de Rasters**
1. **Geração de Previsões**: O modelo treinado é usado para prever valores de NDVI para cada ponto e data.
2. **Criação de Rasters**: As previsões são interpoladas espacialmente (IDW) para gerar arquivos raster `.tif`.

### **Step Four: Relatórios**
1. **Comparação de NDVI**: Comparação entre valores reais e previstos de NDVI.
2. **Visualização**: Um dashboard em Power BI é usado para análise visual dos resultados.