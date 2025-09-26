# Projeto de Ingestão de Dados na Nuvem | NYC Taxi para BigQuery

## Status do Projeto: Fase 1 (Ingestão de Dados) Concluída ✅

## Visão Geral do Projeto

Este projeto de engenharia de dados foca na construção do primeiro estágio de um pipeline de dados moderno (ELT): a extração e carga (Extract & Load). O objetivo é ingerir os dados públicos de viagens de táxi de Nova York (NYC TLC) de uma fonte externa e carregá-los em sua forma bruta no Google BigQuery, preparando o terreno para futuras transformações e análises.

## Problema de Negócio

Para que os dados de viagens de táxi de NY possam ser analisados, eles primeiro precisam ser armazenados de forma centralizada e acessível em um Data Warehouse. Este projeto resolve essa etapa inicial, criando um script robusto que busca os dados na fonte e os deposita em uma tabela no BigQuery, criando uma fonte única da verdade para os dados brutos.

## Arquitetura da Solução (Fase 1: EL)

A solução atual representa a fase de **Extração e Carga (Extract & Load)** de um processo ELT.

**Fluxo de Dados:**

`Fonte de Dados (URL Parquet)` -> `Script Python (Pandas/Requests)` -> `Google BigQuery (Tabela de Dados Brutos)`

1.  **Extração (Extract):** Um script em Python, utilizando a biblioteca `requests`, baixa o arquivo de dados do mês (formato `.parquet`) diretamente da fonte pública.
2.  **Carga (Load):** Utilizando a biblioteca `pandas-gbq`, o script carrega o DataFrame completo para uma tabela de destino no **Google BigQuery**. Esta tabela (`dados_brutos`) serve como a camada Bronze (raw data) do nosso Data Warehouse, garantindo que tenhamos uma cópia fiel dos dados originais na nuvem.

## Tecnologias Utilizadas

- **Linguagem:** Python
- **Bibliotecas Principais:** Pandas, pandas-gbq, Requests
- **Cloud & Data Warehouse:** Google Cloud Platform (GCP), Google BigQuery

## Como Executar

1.  **Pré-requisitos:**
    - Python 3.x instalado.
    - Autenticação da Google Cloud SDK configurada no seu ambiente (`gcloud auth application-default login`).
    - Ter um projeto na GCP com o BigQuery API ativado.
2.  **Clone o Repositório:** `git clone [URL_DO_SEU_REPOSITORIO]`
3.  **Instale as dependências:**
    ```bash
    pip install pandas requests pandas-gbq pyarrow
    ```
4.  **Execute o Notebook:**
    - Abra o notebook `data-pipeline-taxi-nyc-cloud.ipynb`.
    - Altere as variáveis `project_id` e `tabela_destino_bq` para os valores do seu projeto.
    - Execute as células para realizar a ingestão dos dados.

## Próximos Passos (Evolução para um Pipeline ELT Completo)

Com a fase de EL concluída, os próximos passos naturais para este projeto são:

- [ ] **Fase 2 (Transformação):** Utilizar SQL diretamente no BigQuery para criar *views* ou tabelas tratadas (camada Silver) e agregadas (camada Gold) a partir dos dados brutos. Ferramentas como o **dbt** podem ser usadas aqui.
- [ ] **Fase 3 (Automação):** Migrar o script de ingestão para uma **Cloud Function** e usar o **Cloud Scheduler** para automatizar a execução do pipeline mensalmente, tornando-o totalmente autônomo.
- [ ] **Fase 4 (Visualização):** Conectar uma ferramenta de BI, como o **Power BI** ou Looker Studio, às tabelas da camada Gold no BigQuery para criar dashboards analíticos.

## Autor

**Leandro Andrade de Oliveira**
- **LinkedIn:** [linkedin.com/in/leanttro/](https://www.linkedin.com/in/leanttro/)
