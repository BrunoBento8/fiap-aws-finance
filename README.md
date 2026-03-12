# fiap-aws-finance
### Tech Challenge - Fase 2: Pipeline de Dados Bovespa

**Integrantes:**
- Gabriel (Owner)
- Raquel Miranda
- [Adicione os outros nomes aqui]
- [Adicione os outros nomes aqui]
- [Adicione os outros nomes aqui]

#### #### Resumo do Projeto
Este projeto apresenta um pipeline de dados Serverless na AWS para extração, tratamento e análise de dados históricos da B3 (PETR4.SA). O objetivo é automatizar o fluxo de dados desde a captura bruta até a geração de indicadores de negócio, como a Média Móvel.

#### #### Arquitetura
*   **Ingestão:** Script Python utilizando a biblioteca `yfinance` rodando no CloudShell, salvando em **Amazon S3 (Camada RAW)**.
*   **Processamento:** Job em **AWS Glue (PySpark)** para limpeza de colunas, conversão de tipos e cálculo de Média Móvel de 3 dias, salvando em **Amazon S3 (Camada REFINED)**.
*   **Consumo:** **Amazon Athena** para criação de tabela externa e consultas SQL sobre os dados processados.

#### #### Como Executar
1.  **Extração:** Execute o script `scripts_python/extrair_dados.py` para alimentar a pasta `raw/` no S3.
2.  **ETL:** No AWS Glue Studio, crie um Job Spark e utilize o código em `scripts_glue/job_spark_etl.py`.
3.  **Consulta:** No Amazon Athena, execute o DDL contido em `scripts_sql/athena_table.sql` para criar a tabela.
4.  **Validação:** Rode o comando:
    `SELECT * FROM bovespa_refined ORDER BY date DESC;`

#### #### Observações
*   Certifique-se de ajustar o nome do bucket S3 nos scripts para o nome utilizado pelo seu grupo.
*   As permissões de IAM Roles devem incluir acesso ao S3 e CloudWatch Logs.