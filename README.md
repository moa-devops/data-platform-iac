# Modern Data Stack — Big Data Ecosystem com Docker e Terraform

Ambiente de estudo para exploração prática dos principais frameworks de uma plataforma moderna de dados, provisionado com **IaC via Terraform na AWS** e orquestrado com **Docker Compose**.

> **Nota:** Este projeto foi replicado e adaptado a partir do trabalho do [Prof. Fábio Jardim (PUC Minas)](https://github.com/fabiogjardim/mds), no curso de DevOps & Continuous Software Engineering. O objetivo foi reproduzir o ambiente de forma prática para aprofundar o entendimento das ferramentas envolvidas.

![mds](image/front01.png)
![mds](image/front02.png)

---

## Stack de Tecnologias

| Camada | Ferramentas |
|---|---|
| **Infraestrutura** | Terraform, AWS EC2 |
| **Containerização** | Docker, Docker Compose |
| **Ingestão** | Apache NiFi, Debezium (CDC), Kafka (Confluent) |
| **Armazenamento** | MinIO (Data Lake), PostgreSQL |
| **Processamento** | Apache Spark, Apache Hive, Trino |
| **Orquestração** | Apache Airflow |
| **Observabilidade** | Elasticsearch, Kibana |
| **Visualização** | Apache Superset, Metabase, CloudBeaver |

---

## Pré-requisitos

- [Terraform](https://developer.hashicorp.com/terraform/install)
- Conta na [AWS](https://aws.amazon.com/pt/console/)
- [Docker](https://docs.docker.com/install/linux/docker-ce/ubuntu/) instalado no Linux
- [Git](https://git-scm.com/book/pt-br/v2/Começando-Instalando-o-Git)

> A instância recomendada na AWS é **t2.xlarge (16GB RAM)**. Na primeira execução, todas as imagens serão baixadas automaticamente.

---

## Setup

**1. Provisionar a infraestrutura com Terraform**

```bash
cd Terraform
terraform init
terraform apply
```

**2. Clonar o repositório na instância AWS**

```bash
git clone https://github.com/moa-devops/mds.git
cd mds
```

---

## Iniciando o Ambiente

É recomendado subir apenas os serviços do workload que será utilizado.

**Data Lake + Spark**
```bash
docker-compose up -d minio spark-worker
```

**CDC com Kafka + PostgreSQL**
```bash
docker-compose up -d minio kafka-broker kafka-connect nifi postgres
```

**Todos os containers** *(requer 16GB+ de RAM)*
```bash
docker-compose up -d
```

---

## Comandos Úteis

```bash
# Verificar containers em execução
docker ps

# Parar um container
docker stop <nome>

# Parar todos os containers
docker stop $(docker ps -a -q)

# Remover todos os containers
docker rm $(docker ps -a -q)

# Inspecionar um container
docker container inspect <nome>

# Ver logs de um container
docker container logs <nome>
```

---

## Acesso às Interfaces Web

| Serviço | Endereço |
|---|---|
| MinIO | http://IP-da-AWS:9051 |
| Jupyter Spark | http://IP-da-AWS:8889 |
| Apache Pinot | http://IP-da-AWS:9000 |
| NiFi | http://IP-da-AWS:9090 |
| Kafka Control Center | http://IP-da-AWS:9021 |
| Airflow | http://IP-da-AWS:8180 |
| Elasticsearch | http://IP-da-AWS:9200 |
| Metabase | http://IP-da-AWS:3000 |
| Kibana | http://IP-da-AWS:5601 |
| Superset | http://IP-da-AWS:8088 |
| Trino | http://IP-da-AWS:8080 |
| CloudBeaver | http://IP-da-AWS:8010 |

---

## Credenciais Padrão

| Serviço | Usuário | Senha |
|---|---|---|
| Superset | admin | admin |
| Metabase | admin@mds.com | admin |
| PostgreSQL | admin | admin |
| MinIO | admin | admin |
| Pinot | admin | admin |
| Kibana | admin | admin |
| CloudBeaver | admin | admin |

---

## Documentação Oficial

- [CloudBeaver](https://dbeaver.com/docs/cloudbeaver/Run-Docker-Container/)
- [Trino](https://trino.io/docs/current/installation/containers.html)
- [Superset](https://superset.apache.org/docs/installation/installing-superset-using-docker-compose/)
- [Metabase](https://www.metabase.com/docs/latest/installation-and-operation/running-metabase-on-docker)
- [Delta Lake](https://delta.io/)
- [MinIO](https://min.io/docs/minio/container/operations/installation.html)
- [Elasticsearch](https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html)
- [PostgreSQL](https://github.com/docker-library/postgres)
- [Pinot](https://docs.pinot.apache.org/basics/getting-started/running-pinot-in-docker)
- [Jupyter Spark](https://jupyter-docker-stacks.readthedocs.io/en/latest/using/specifics.html)
- [Airflow](https://airflow.apache.org/docs/apache-airflow/stable/howto/docker-compose/index.html)
- [Kafka Confluent](https://docs.confluent.io/platform/current/installation/docker/installation.html)
- [Debezium](https://debezium.io/documentation/reference/stable/docker.html)
- [NiFi](https://hub.docker.com/r/apache/nifi)
- [Imagens no Docker Hub](https://hub.docker.com/u/fjardim)

---

## Créditos

Projeto baseado no repositório do [Prof. Fábio Jardim](https://github.com/fabiogjardim/mds) — PUC Minas, curso de DevOps & Continuous Software Engineering.
