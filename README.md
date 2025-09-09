# Projeto de Detecção de Anomalias em Churn de Clientes

## Descrição do Projeto

Este projeto implementa um sistema de detecção de anomalias utilizando o algoritmo **Local Outlier Factor (LOF)** para identificar padrões anômalos nos dados de churn de clientes de uma empresa de telecomunicações. O objetivo principal é detectar clientes com comportamentos atípicos que possam indicar maior probabilidade de cancelamento dos serviços.

## Objetivos

- **Objetivo Principal**: Identificar anomalias nos dados de clientes que possam estar relacionadas ao churn
- **Objetivo Secundário**: Maximizar o True Positive Rate (TPR) através da métrica de recall para detectar efetivamente os casos de churn
- **Aplicação Prática**: Fornecer insights para estratégias de retenção de clientes

## Dataset

O projeto utiliza o dataset `churn_telecom.csv` que contém informações sobre clientes de uma empresa de telecomunicações, incluindo:

### Variáveis do Dataset:
- **IDCliente**: Identificador único do cliente
- **Churn**: Variável target (Yes/No) - indica se o cliente cancelou o serviço
- **tenure**: Tempo de permanência do cliente (em meses)
- **MonthlyCharges**: Cobrança mensal
- **TotalCharges**: Cobrança total
- **Genero**: Gênero do cliente
- **TemParceiro**: Se o cliente tem parceiro (Yes/No)
- **TemDependentes**: Se o cliente tem dependentes (Yes/No)
- **PhoneService**: Se possui serviço telefônico (Yes/No)
- **MultipleLines**: Se possui múltiplas linhas
- **InternetService**: Tipo de serviço de internet
- **OnlineSecurity**: Se possui segurança online (Yes/No)
- **OnlineBackup**: Se possui backup online (Yes/No)
- **DeviceProtection**: Se possui proteção de dispositivo (Yes/No)
- **TechSupport**: Se possui suporte técnico (Yes/No)
- **StreamingTV**: Se possui TV streaming (Yes/No)
- **StreamingMovies**: Se possui streaming de filmes (Yes/No)
- **Contract**: Tipo de contrato
- **PaperlessBilling**: Se possui cobrança sem papel (Yes/No)
- **PaymentMethod**: Método de pagamento
- **Mais65anos**: Se o cliente tem mais de 65 anos

## Metodologia

### 1. Pré-processamento dos Dados
- **Remoção de variáveis**: IDCliente e Churn (target) são removidos do conjunto de features
- **Transformações aplicadas**:
  - **Variáveis Numéricas**: Padronização usando StandardScaler
  - **Variáveis Categóricas**: Codificação One-Hot usando OneHotEncoder
  - **Variáveis Binárias**: Transformação customizada (Yes → 1, No → 0)
  - **Sem Transformação**: Variáveis já numéricas como 'Mais65anos'

### 2. Algoritmo LOF (Local Outlier Factor)
- **Parâmetros utilizados**:
  - `n_neighbors=20`: Número de vizinhos para cálculo da densidade local
  - `contamination=0.26`: Proporção esperada de anomalias nos dados

### 3. Avaliação
- **Métrica principal**: Recall Score
- **Justificativa**: Maximizar a detecção de verdadeiros positivos (casos de churn)

## Estrutura do Projeto

```
projeto-deteccao-anomalias/
│
├── deteccao_anomalias.ipynb          # Notebook principal com a análise
├── churn_telecom.csv                 # Dataset de clientes de telecomunicações
├── dataset.csv                       # Dataset adicional
├── gmm.ipynb                         # Notebook com algoritmo GMM
├── modelo_clusterizacao_clientes_gmm.pkl      # Modelo GMM salvo
├── pipeline_clusterizacao_clientes_gmm.pkl   # Pipeline GMM salvo
├── requirements.txt                  # Dependências do projeto
└── README.md                        # Este arquivo
```

## Instalação e Configuração
OBS: Caso queira optar por executar em ambientes como Google collab ou Anaconda jupyter, basta descomentar a primeira célula do arquivo ipynb e executar o arquivo caso esteja faltando alguma dependencia. É uma alternativa ao arquivo requirements.txt.

### Pré-requisitos
- Python 3.12 ou superior
- Jupyter Notebook ou JupyterLab

### Instalação das Dependências

1. Clone ou faça download do projeto
2. Instale as dependências:

```bash
pip install -r requirements.txt
```

### Executando o Projeto

1. Abra o Jupyter Notebook:
```bash
jupyter notebook
```

2. Navegue até o arquivo `deteccao_anomalias.ipynb`
3. Execute as células sequencialmente

## Principais Bibliotecas Utilizadas

- **pandas**: Manipulação e análise de dados
- **numpy**: Operações numéricas
- **plotly**: Visualizações interativas
- **scikit-learn**: Algoritmos de machine learning
  - LocalOutlierFactor: Algoritmo principal de detecção de anomalias
  - StandardScaler: Padronização de dados
  - OneHotEncoder: Codificação de variáveis categóricas
  - ColumnTransformer: Pipeline de transformações
  - recall_score: Métrica de avaliação

## Resultados Esperados

O algoritmo LOF irá:
1. **Identificar anomalias** nos dados de clientes
2. **Classificar cada cliente** como:
   - `-1`: Anomalia (comportamento atípico)
   - `1`: Normal (comportamento típico)
3. **Calcular o score LOF** para cada cliente (negative_outlier_factor_)
4. **Avaliar a performance** usando recall score

### Interpretação dos Resultados
- **Anomalias detectadas**: Clientes com padrões comportamentais únicos
- **Score LOF**: Quanto menor (mais negativo), mais anômalo é o ponto
- **Recall Score**: Indica a capacidade do modelo de detectar casos reais de churn

## Aplicações Práticas

1. **Retenção de Clientes**: Identificar clientes com alto risco de churn
2. **Segmentação**: Criar grupos especiais para clientes anômalos
3. **Estratégias Personalizadas**: Desenvolver abordagens específicas para cada tipo de anomalia
4. **Monitoramento**: Acompanhar mudanças nos padrões de comportamento dos clientes

## Limitações e Considerações

- O algoritmo LOF é sensível à escolha dos parâmetros `n_neighbors` e `contamination`
- A performance pode variar dependendo da distribuição dos dados
- É importante validar os resultados com conhecimento de domínio
- Anomalias detectadas nem sempre indicam churn real

## Licença

Este projeto é de código aberto e está disponível sob a licença MIT.

