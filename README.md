# NDVI Prediction 

Este repositório contém um pipeline completo para a previsão do Índice de Vegetação por Diferença Normalizada (NDVI) utilizando dados de satélite Sentinel-1, Sentinel-2. O objetivo principal é gerar previsões de NDVI e compará-las com valores reais para análise e tomada de decisão.

## Por que usar o NDVI Prediction ?

O NDVI é uma métrica amplamente utilizada para monitorar a saúde da vegetação, identificar padrões de crescimento e avaliar o impacto de condições climáticas. No entanto, a obtenção de dados confiáveis de NDVI pode ser desafiadora devido à presença de nuvens, que frequentemente obscurecem as imagens de satélite, especialmente em regiões tropicais.

Com o NDVI Prediction, é possível superar essa limitação ao prever valores de NDVI diariamente, mesmo em dias nublados. A abordagem combina dados históricos de NDVI e dados de radar (como os do Sentinel-1, que não são afetados por nuvens) para gerar previsões precisas. Isso garante:

- **Cobertura Contínua**: Dados diários de NDVI, independentemente das condições climáticas.
- **Tomada de Decisão Rápida**: Informações atualizadas para apoiar decisões em agricultura, manejo de recursos naturais e monitoramento ambiental.
- **Redução de Lacunas**: Preenchimento de períodos sem dados devido à cobertura de nuvens, garantindo séries temporais completas e consistentes.

Essa abordagem é especialmente útil para agricultores, pesquisadores e gestores ambientais que precisam de dados confiáveis e frequentes para planejar ações e responder rapidamente a mudanças no ambiente.

## Fluxograma do projeto

![alt text](<Sem título-2023-12-04-1708.png>)

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