# Análise estatística de base de dados de diabetes

Os dois arquivos IPython Notebook fornecidos abordam o processamento e a análise exploratória de dados (EDA) de um conjunto de dados sobre indicadores de saúde relacionados ao diabetes, proveniente do Sistema de Vigilância de Fatores de Risco Comportamentais (BRFSS) de 2015, disponibilizado no Kaggle. Abaixo, apresento um resumo com os principais resultados e etapas realizadas em cada documento.

## Primeiro Documento: Pré-processamento de Dados
Este documento foca na preparação inicial do conjunto de dados para análise, incluindo leitura, limpeza, transformação e otimização.

1. Descrição do Conjunto de Dados
* Fonte: Pesquisa BRFSS 2015 (CDC), com dados sobre condições crônicas, comportamentos de risco e uso de serviços preventivos.
* Tamanho: 70.692 registros e 22 colunas.
* Variáveis: Incluem indicadores binários (ex.: Diabetes_binary, HighBP), numéricos (ex.: BMI, MentHlth) e categóricos ordenados (ex.: GenHlth, Age).
2. Pré-processamento
* Leitura: Dados carregados de um arquivo CSV compactado usando pandas.
* Renomeação de Colunas: As colunas foram traduzidas para português (ex.: Diabetes_binary → Diabetes, HighBP → PressaoAlta) para facilitar a interpretação.
* Conversão de Tipos:
    * Variáveis binárias (0 ou 1) foram convertidas para tipo category.
    * Variáveis categóricas ordenadas (ex.: SaudeGeral, FaixaIdade) foram transformadas em categorias com rótulos descritivos (ex.: SaudeGeral: 1 = "Excelente", 5 = "Ruim").
    * Variáveis numéricas (ex.: IMC, DiasProblemasMentais) foram otimizadas para int8 quando inteiros, reduzindo o uso de memória.
* Otimização: O DataFrame foi salvo em formato parquet, reduzindo o tamanho do arquivo e melhorando a eficiência de leitura.
3. Estatísticas Descritivas
* Numéricas:
    * IMC: Média ≈ 29,86, desvio padrão ≈ 7,11, intervalo de 12 a 98.
    * DiasProblemasMentais: Média ≈ 3,75, mediana = 0, máximo = 30.
    * DiasProblemasFisicos: Média ≈ 5,81, mediana = 0, máximo = 30.
* Categóricas:
    * Diabetes: 50% "Não" e 50% "Sim" (balanceado).
    * PressaoAlta: 56,3% "Sim".
    * SaudeGeral: "Boa" (33,1%) é a categoria mais frequente.
    * FaixaIdade: "65-69" (15,4%) é a faixa mais comum.
4. Resultados Principais
* O conjunto foi limpo e organizado com colunas renomeadas e tipos ajustados, ocupando apenas 1,5 MB após otimização (originalmente 11,9 MB).
Variáveis numéricas como DiasProblemasMentais e DiasProblemasFisicos têm forte assimetria à direita (mediana = 0, mas com máximos em 30), sugerindo presença de outliers.

### Segundo Documento: Análise Exploratória de Dados (EDA)
Este documento realiza uma análise exploratória inicial, carregando os dados tratados do primeiro documento e examinando variáveis numéricas e categóricas.

1. Carregamento e Estrutura
* Dados lidos do arquivo parquet gerado anteriormente.
* Confirmação da estrutura: 70.692 linhas, 22 colunas, com 19 categóricas e 3 numéricas (IMC, DiasProblemasMentais, DiasProblemasFisicos).
2. Classificação das Variáveis
* Numéricas: IMC, DiasProblemasMentais, DiasProblemasFisicos.
* Categóricas:
    * Binárias (2 valores): Ex.: PressaoAlta, Fumante, AtividadeFisica (14 no total).
    * Não Binárias (>2 valores): SaudeGeral, FaixaIdade, Ensino, FaixaRenda.
    * Alvo: Diabetes (binária: "Sim" ou "Não").
3. Análise de Correlação (Parcial)
* Um mapa de calor com coeficientes de Spearman foi gerado para variáveis categóricas, mas o código está incompleto no documento fornecido (falta a definição de resultados_correlacao). Presume-se que o objetivo era explorar associações entre variáveis categóricas e o alvo Diabetes.
4. Resultados Preliminares
* A segmentação das variáveis facilita análises futuras (ex.: testes estatísticos para binárias, análises ordinais para não binárias).
Não há resultados completos de EDA devido à interrupção do código, mas o mapa de calor sugere interesse em correlações como PressaoAlta ou SaudeGeral com Diabetes.


![imagem](imagens/diabetes.jpg)

## Organização do projeto

```
├── .gitignore         <- Arquivos e diretórios a serem ignorados pelo Git
├── ambiente.yml       <- O arquivo de requisitos para reproduzir o ambiente de análise
├── LICENSE            <- Licença de código aberto (MIT)
├── README.md          <- README principal para desenvolvedores que usam este projeto.
|
├── dados              <- Arquivos de dados para o projeto.
|
├── notebooks          <- Jupyter Notebooks.
│
|   └──src             <- Código-fonte para uso neste projeto.
|      │
|      ├── __init__.py  <- Torna um módulo Python
|      ├── config.py    <- Configurações básicas do projeto
|      └── estatistica.py  <- Funções criadas especificamente para este projeto
|
├── referencias        <- Dicionários de dados.
|
├── imagens            <- Imagens utilizadas no projeto
```

## Configuração do ambiente

1. Faça o clone do repositório.

    ```bash
    git clone git@github.com:exemplohashtag/projeto_teste.git
    ```

2. Crie um ambiente virtual para o seu projeto utilizando o `conda`.

   ```bash
   conda env create -f ambiente.yml --name estatistica
   ```

## Um pouco mais sobre a base

[Clique aqui](referencias/01_dicionario_de_dados.md) para ver o dicionário de dados da base utilizada.

## Conclusões Gerais
1. Pré-processamento: O primeiro documento preparou os dados de forma eficiente, reduzindo o uso de memória e tornando as variáveis mais interpretáveis com nomes em português e categorias descritivas.
2. EDA Inicial: O segundo documento começou a análise exploratória, destacando a estrutura das variáveis e preparando o terreno para investigações mais profundas, como correlações e testes estatísticos.
3. Principais Observações:
    * O conjunto é balanceado em relação a Diabetes (50%/50%), o que é ideal para modelagem preditiva.
    * Variáveis como IMC e dias de problemas de saúde mostram distribuições assimétricas, indicando a necessidade de tratamento de outliers ou transformações.
    * A prevalência de condições como pressão alta (56,3%) e colesterol alto (52,6%) sugere fatores de risco comuns associados ao diabetes.
