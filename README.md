# Análise Estatística de Dados de Preços de Moradias na Califórnia

Este projeto aborda a análise exploratória de dados (EDA) e o processamento de um conjunto de dados sobre preços de moradias na Califórnia, derivado do censo dos EUA de 1990. Os dados foram obtidos do Kaggle e estão disponíveis no seguinte link: [California Housing Prices](https://www.kaggle.com/datasets/camnugent/california-housing-prices/data).

## Descrição do Conjunto de Dados

O conjunto de dados contém informações sobre grupos de blocos censitários na Califórnia, a menor unidade geográfica para a qual o Escritório do Censo dos EUA publica dados amostrais (geralmente com populações de 600 a 3.000 pessoas). Cada linha representa um grupo de blocos, e os dados incluem variáveis relacionadas a características demográficas, geográficas e habitacionais.

### Detalhes do Conjunto de Dados
- **Fonte**: Censo dos EUA de 1990.
- **Unidade**: Grupos de blocos censitários.
- **Variáveis Principais**:
  - `median_house_value`: Valor mediano das casas no grupo de blocos (em dólares, variável alvo).
  - `median_income`: Renda mediana no grupo de blocos (em dezenas de milhares de dólares).
  - `housing_median_age`: Idade mediana das casas no grupo de blocos.
  - `total_rooms`: Número total de cômodos no grupo de blocos.
  - `total_bedrooms`: Número total de quartos no grupo de blocos.
  - `population`: População do grupo de blocos.
  - `households`: Número de domicílios no grupo de blocos.
  - `latitude`: Latitude do grupo de blocos.
  - `longitude`: Longitude do grupo de blocos.
  - `ocean_proximity`: Proximidade do oceano (categórica: "NEAR BAY", "<1H OCEAN", "INLAND", "NEAR OCEAN", "ISLAND").
- **Notas**:
  - Um domicílio (*household*) é um grupo de pessoas que reside em uma casa.
  - Variáveis como `total_rooms` e `total_bedrooms` são médias por domicílio, o que pode levar a valores altos em áreas com poucos domicílios e muitas casas vazias (ex.: resorts de férias).

## Organização do Projeto

```
├── .gitignore         <- Arquivos e diretórios a serem ignorados pelo Git
├── ambiente.yml       <- O arquivo de requisitos para reproduzir o ambiente de análise
├── LICENSE            <- Licença de código aberto (MIT)
├── README.md          <- README principal para desenvolvedores que usam este projeto
|
├── dados              <- Arquivos de dados para o projeto
|
├── notebooks          <- Jupyter Notebooks
│
|   └── src            <- Código-fonte para uso neste projeto
|      │
|      ├── __init__.py  <- Torna um módulo Python
|      ├── config.py    <- Configurações básicas do projeto
|      └── estatistica.py  <- Funções criadas especificamente para este projeto
|
├── referencias        <- Dicionários de dados
|
├── imagens            <- Imagens utilizadas no projeto
```

## Configuração do Ambiente

1. Faça o clone do repositório:

    ```bash
    git clone git@github.com:Lgleidson/projeto_ds_housing.git
    ```

2. Crie um ambiente virtual para o seu projeto utilizando o `conda`:

   ```bash
   conda env create -f ambiente.yml --name housing_analysis
   ```

## Um Pouco Mais Sobre a Base

[Clique aqui](referencias/01_dicionario_de_dados.md) para ver o dicionário de dados da base utilizada.

## Análise Realizada

*Esta seção será preenchida conforme a análise exploratória e o processamento dos dados forem realizados. Por enquanto, o foco está na preparação do ambiente e na familiarização com o conjunto de dados.*

### Possíveis Etapas Futuras
1. **Pré-processamento**:
   - Carregar os dados e verificar valores ausentes (ex.: `total_bedrooms` pode ter dados faltantes, conforme comum neste dataset).
   - Tratar variáveis categóricas como `ocean_proximity` (ex.: codificação one-hot).
   - Normalizar variáveis numéricas como `median_income` e `total_rooms` para lidar com escalas diferentes.
2. **Análise Exploratória de Dados (EDA)**:
   - Examinar distribuições de variáveis como `median_house_value` e `median_income`.
   - Investigar correlações entre variáveis (ex.: `median_income` vs. `median_house_value`).
   - Visualizar a distribuição geográfica dos preços usando `latitude` e `longitude`.
3. **Modelagem**:
   - Testar modelos preditivos para prever `median_house_value` (ex.: regressão linear, árvores de decisão).
   - Avaliar o impacto de variáveis como `ocean_proximity` e `median_income` no valor das casas.

## Observações Iniciais
- A variável alvo `median_house_value` pode ter valores limitados no topo (ex.: capped em $500,000), um artefato comum neste conjunto de dados.
- Variáveis como `total_rooms` e `total_bedrooms` podem apresentar distribuições assimétricas devido à média por domicílio, exigindo transformações (ex.: log) ou criação de novas variáveis (ex.: cômodos por pessoa).
- A proximidade do oceano (`ocean_proximity`) provavelmente tem forte influência nos preços das casas, o que pode ser explorado em análises futuras.
