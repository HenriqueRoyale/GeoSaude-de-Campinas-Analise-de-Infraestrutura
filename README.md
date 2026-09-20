# 🏥 GeoSaúde Campinas: Análise de Infraestrutura (ODS 3)

[![Python 3.10+](https://img.shields.io/badge/Python-3.10%2B-3776AB.svg?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![MongoDB Atlas](https://img.shields.io/badge/MongoDB-Atlas-47A248.svg?style=for-the-badge&logo=mongodb&logoColor=white)](https://www.mongodb.com/)
[![Dash](https://img.shields.io/badge/UI-Dash%20Plotly-3FB27F.svg?style=for-the-badge&logo=plotly&logoColor=white)](https://dash.plotly.com/)
[![NetworkX](https://img.shields.io/badge/Graph-NetworkX-00599C.svg?style=for-the-badge)](https://networkx.org/)

> Uma plataforma de integração de dados e análise geoespacial focada na **Infraestrutura de Saúde Pública do município de Campinas (ODS 3)**[cite: 1]. O projeto realiza a extração automatizada de dados públicos, tratamento em formato GeoJSON, armazenamento em banco NoSQL estruturado e exibe os resultados em um Dashboard analítico com grafos de rede[cite: 1].

---

## 🎯 Sobre o Projeto

Este projeto interdisciplinar explora o uso de Bancos de Dados Não Relacionais (MongoDB) para resolver desafios de mapeamento de infraestrutura[cite: 1]. A aplicação coleta dados de saúde via API do CNES (DataSUS) e informações demográficas pelo IBGE[cite: 1]. 

O grande destaque técnico é a elaboração de um **Grafo de Referência/Contrarreferência**, conectando geograficamente Unidades Básicas de Saúde (Atenção Primária) aos Hospitais mais próximos (Atenção Terciária) utilizando pipelines do MongoDB (`$geoNear`) e cálculos de centralidade do NetworkX[cite: 1].

### 🌟 Destaques do Projeto
- 🗺️ **Índices Geoespaciais (`2dsphere`):** Localização em alta resolução de unidades de saúde baseadas em latitude/longitude[cite: 1].
- 🕸️ **Análise de Grafos (NetworkX):** Identificação de hospitais que atuam como "nós centrais" de recebimento de pacientes via métrica de *In-Degree Centrality*[cite: 1].
- 📊 **Interface Dashboard Interativa:** Aplicação Dash/Plotly em *Dark Mode* monitorando KPIs, abrangência do SUS e mapas interativos com atualizações automáticas[cite: 1].
- 🍃 **Pipelines de Agregação:** Processamento direto no banco de dados para dedup de registros, união de dados (UBS e Hospitais) e cálculos de métricas de acesso[cite: 1].

---

## 🧠 Como Funciona a Arquitetura de Dados

O sistema integra dados brutos de APIs federais, aplica transformações ETL e os injeta em coleções do MongoDB Atlas[cite: 1].

```text
                            [ APIs Públicas (CNES / IBGE) ]
                                          │
                            [ Pipeline ETL (Pandas/Python) ] ◄── Limpeza, Tipagem e GeoJSON
                                          │
                                 [ MongoDB Atlas ] ◄── Coleções: estabelecimentos, setores, relacionamentos
                                  /               \
                 [ Agregações e Índices Geo ]   [ Grafo $geoNear (UBS → Hospital) ]
                                  \               /
                              [ Servidor Dash / Plotly ] ◄── Live updates a cada 30s
                                          │
                             [ Dashboard Web Interativo ]

```

### 📈 KPIs Monitorados

Através da `Aggregation Framework`, a plataforma levanta métricas vitais:

1. **Cobertura SUS:** Proporção de estabelecimentos públicos vs. privados.


2. **Estatísticas de Deslocamento:** Distâncias mínima, média e máxima (em km) que um usuário do SUS precisaria percorrer de uma UBS até o hospital de referência.


3. **Distribuição Territorial:** Densidade de clínicas e top 10 bairros com mais infraestrutura de saúde.



---

## 🛠️ Tecnologias Utilizadas

* **Linguagem:** Python 3.10+
* **Bancos de Dados NoSQL:** MongoDB Atlas, PyMongo


* **ETL e Engenharia de Dados:** Pandas, NumPy, API Requests


* **Visualização & Grafos:** Dash, Plotly Express, NetworkX



---

## 📂 Estrutura do Repositório

```text
GeoSaude-Campinas/
├── app_dashboard.py      # Aplicação Web Dash (Métricas, Gráficos e Mapas)
├── etl_mongodb.py        # Pipeline de coleta, tratamento e ingestão de dados
├── requirements.txt      # Dependências (pymongo, dash, pandas, networkx, etc.)
└── README.md             # Documentação do projeto

```

*(Nota: no escopo acadêmico atual, o código pode se encontrar consolidado no notebook do projeto integrador)*.

---

## 🚀 Como Executar o Projeto

### 📋 Pré-requisitos

* Ter o **Python 3.10+** instalado.
* Possuir uma conta e um cluster ativo no **MongoDB Atlas**, garantindo que o *Network Access* esteja liberado para `0.0.0.0/0`.



### 1. Clonar o Repositório

```bash
git clone [https://github.com/HenriqueRoyale/GeoSaude-Campinas.git](https://github.com/HenriqueRoyale/GeoSaude-Campinas.git)
cd GeoSaude-Campinas

```

### 2. Instalar as Dependências

```bash
pip install -r requirements.txt
# ou manualmente: pip install pymongo[srv] dnspython certifi pandas tqdm requests dash plotly networkx

```

### 3. Configurar Credenciais (URI do Mongo)

Exporte a variável de ambiente com a sua *Connection String* do MongoDB Atlas.

* **Linux/Mac:** `export MONGO_URI="sua_uri_aqui"`
* **Windows (CMD):** `set MONGO_URI="sua_uri_aqui"`

### 4. Executar os Módulos

#### 🔄 Modo 1: Carga de Dados (ETL)

Execute o script de coleta para formatar os dados do DataSUS/IBGE e provisionar o banco de dados:

```bash
python etl_mongodb.py

```

#### 🌐 Modo 2: Iniciar Dashboard Interativo

Levante o servidor de interface visual com Dash:

```bash
python app_dashboard.py

```

Acesse em seu navegador padrão através de `http://127.0.0.1:8050`.

---

## 👥 Autores

**Projeto Integrador e Extensionista — PUC-Campinas**

* **Integrantes:** Bruno de Souza, Henrique Silvestre, Igor, Lucas Garrido, Lucas Rosário


* **Docente Responsável:** Felipe Cavalaro


* **GitHub:** [@HenriqueRoyale](https://github.com/HenriqueRoyale?utm_source=gemini)

```

```
