# Mineração-Dados
# Perfil Institucional e Docente do Ensino Superior Brasileiro em 2024

Este repositório reúne o notebook, os códigos desenvolvidos para a análise do perfil institucional e docente das Instituições de Ensino Superior (IES) brasileiras em 2024, utilizando os microdados públicos do Censo da Educação Superior disponibilizados pelo INEP.

O estudo aplica técnicas de mineração de dados para analisar diferenças entre IES públicas e privadas, considerando indicadores de titulação docente, regime de trabalho, porte institucional, composição etária e situação das licenciaturas.

## Arquivos do repositório

```text
.
├── Mineração_Dados.ipynb
├── MicroDAdos.zip
├── dicionário_dados_educação_superior
└── README.md
```

### `Mineração_Dados.ipynb`

Notebook principal do projeto. Ele contém todas as etapas da análise:

1. leitura da base de IES;
2. criação dos indicadores docentes;
3. geração dos gráficos exploratórios;
4. treinamento do SVM com dois atributos;
5. treinamento do SVM com sete atributos;
6. visualização por PCA;
7. clusterização das licenciaturas com K-Means;
8. estudo de caso das IES de Uberlândia.

### `figs/`

Pasta sugerida para armazenar os gráficos gerados pelo notebook em formato PDF utilizado no artigo.

## Bases de dados utilizadas

As bases utilizadas são públicas e foram obtidas nos microdados do Censo da Educação Superior de 2024, disponibilizados pelo INEP.

Foram utilizados principalmente os seguintes arquivos:

```text
MICRODADOS_ED_SUP_IES_2024.CSV
MICRODADOS_CADASTRO_CURSOS_2024.CSV
```

A base de IES foi utilizada para caracterizar o perfil institucional e docente das instituições. A base de cursos foi utilizada para filtrar os cursos de licenciatura e construir indicadores de procura, permanência, conclusão, trancamento e desvinculação.

## Atenção sobre a pasta dos dados

O notebook foi desenvolvido originalmente no Google Colab. Por isso, antes de executar o notebook, o usuário deve alterar o caminho da pasta onde estão os microdados.

No notebook, localize o trecho abaixo:

```python
from google.colab import drive
drive.mount('/content/drive')

pasta_dados = "/content/drive/MyDrive/Dados/MINERACAO"
```

Altere o valor de `pasta_dados` para o local onde os arquivos CSV foram salvos no seu ambiente.

Exemplo no Google Colab:

```python
pasta_dados = "/content/drive/MyDrive/Dados/MINERACAO"
```

Exemplo em ambiente local:

```python
pasta_dados = "C:/Users/SEU_USUARIO/Documents/Dados/MINERACAO"
```

Depois disso, o notebook monta automaticamente os caminhos dos arquivos:

```python
caminho_ies = f"{pasta_dados}/MICRODADOS_ED_SUP_IES_2024.CSV"
caminho_cursos = f"{pasta_dados}/MICRODADOS_CADASTRO_CURSOS_2024.CSV"
```

Portanto, a pasta indicada em `pasta_dados` deve conter os dois arquivos CSV com esses nomes.

## Dependências

O projeto foi desenvolvido em Python, utilizando principalmente as seguintes bibliotecas:

```text
pandas
numpy
matplotlib
seaborn
scikit-learn
```

Para instalar as dependências em ambiente local, execute:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn
```

No Google Colab, essas bibliotecas geralmente já estão disponíveis.

## Como executar

1. Baixe os microdados do Censo da Educação Superior 2024 no portal do INEP.
2. Extraia os arquivos CSV necessários.
3. Coloque os arquivos na pasta desejada.
4. Abra o notebook `Mineração_Dados.ipynb`.
5. Ajuste a variável `pasta_dados`.
6. Execute os blocos na ordem em que aparecem no notebook.

## Indicadores construídos

A análise utiliza indicadores percentuais calculados a partir dos dados agregados por IES, como:

- percentual de docentes doutores;
- percentual de docentes mestres;
- percentual de docentes com formação stricto sensu;
- percentual de docentes em dedicação exclusiva;
- percentual de docentes em regime parcial;
- percentual de docentes horistas;
- idade média estimada do corpo docente;
- indicadores de procura, permanência e conclusão nas licenciaturas.

O indicador de formação stricto sensu foi calculado pela soma dos percentuais de docentes mestres e doutores.

## Técnicas utilizadas

O projeto utiliza diferentes técnicas de mineração de dados:

### Análise exploratória

Foram gerados gráficos para comparar os setores público e privado quanto à composição etária, escolaridade docente, titulação e regime de trabalho.

### SVM com dois atributos

Foi treinado um modelo de Máquinas de Vetores de Suporte com dois atributos:

- percentual de docentes com formação stricto sensu;
- percentual de docentes em dedicação exclusiva.

Esse modelo foi utilizado para visualizar a separabilidade inicial entre IES públicas e privadas.

### SVM com sete atributos

Foi treinado um segundo modelo SVM com sete atributos, incorporando variáveis de titulação, regime de trabalho, porte institucional e composição etária.

O modelo ampliado apresentou melhor desempenho, especialmente na identificação das IES públicas.

### PCA

A Análise de Componentes Principais foi utilizada apenas como recurso de visualização bidimensional do modelo com sete atributos. As métricas foram calculadas com base no SVM treinado com os atributos originais.

### K-Means nas licenciaturas

Foi aplicado K-Means para agrupar IES com cursos de licenciatura segundo indicadores de procura, permanência e conclusão.

Foram testados diferentes valores de `k`, e a escolha final considerou o equilíbrio entre desempenho quantitativo e interpretabilidade dos grupos.

### Estudo de caso: Uberlândia

Foi realizado um recorte local das IES situadas em Uberlândia, combinando indicadores de perfil docente com informações sobre cursos de licenciatura.

Esse recorte permite observar, em escala municipal, como a qualificação docente, a existência de licenciaturas e a permanência dos estudantes se relacionam.

## Principais resultados

Os resultados indicaram diferenças estruturais entre os setores público e privado. As IES públicas apresentaram maior concentração relativa de docentes doutores e maior presença de vínculos em dedicação exclusiva. As IES privadas apresentaram maior heterogeneidade institucional e maior participação de vínculos mais flexíveis.

O modelo SVM com sete atributos apresentou desempenho superior ao modelo com dois atributos, principalmente na identificação da classe pública.

Na análise das licenciaturas, os agrupamentos obtidos por K-Means indicaram perfis distintos de procura, permanência e conclusão, sugerindo possíveis fragilidades no fluxo de formação inicial docente.

## Observação sobre os dados

Os dados utilizados são transversais e agregados por instituição. Assim, os resultados não acompanham trajetórias individuais de docentes ou estudantes ao longo do tempo e não permitem inferências causais.

As análises devem ser interpretadas como evidências quantitativas e exploratórias sobre padrões institucionais do ensino superior brasileiro em 2024.

## Referência dos dados

Instituto Nacional de Estudos e Pesquisas Educacionais Anísio Teixeira (INEP). Microdados do Censo da Educação Superior 2024.

## Autor

Abadio de Paulo Silva  
Programa de Pós-Graduação em Ciência da Computação  
Universidade Federal de Uberlândia
