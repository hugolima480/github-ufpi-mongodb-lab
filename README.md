# 🍃 Laboratório de Banco de Dados NoSQL: MongoDB em AWS EC2

Repositório destinado à documentação e execução do ambiente cliente para o trabalho prático da disciplina de **Banco de Dados Não Convencionais**, do curso de Tecnologia de Gestão de Dados da **Universidade Federal do Piauí (UFPI)**.

## 📌 Sobre o Projeto
Este laboratório demonstra a implementação de um ambiente de banco de dados NoSQL baseado em MongoDB numa infraestrutura de nuvem (AWS Academy). O projeto baseia-se num modelo **Client-Server** focado no isolamento de recursos, em que o processamento de dados ocorre de forma segura na nuvem, e a camada de gerência opera através deste ambiente cliente.

## 🛠️ Tecnologias Utilizadas
* **Banco de Dados:** MongoDB v7.0
* **Nuvem:** AWS EC2 (Ubuntu Server 24.04 LTS)
* **Conteinerização:** Docker
* **Administração Gráfica:** Mongo Express
* **Ambiente Cliente:** GitHub Codespaces / Linux (Crostini)

## 🔒 Arquitetura e Segurança
A infraestrutura foi configurada seguindo os princípios de *Zero Trust*:
* **Security Group (AWS):** Tráfego das portas `22` (SSH) e `27017` (MongoDB) restrito exclusivamente ao IP público da máquina cliente.
* **Autenticação:** Diretiva `security: authorization: "enabled"` ativa no ficheiro `mongod.conf`, forçando o uso de credenciais em qualquer transação.
* **Conexão Remota:** Exposição do daemon controlada através da diretiva `bindIp: 0.0.0.0` para comunicação com o ambiente de administração.

## ⚙️ Destaques da Implementação
* **Modelagem Relacional em NoSQL:** Criação das coleções `cursos` e `alunos` com validação de dados cruzados.
* **Operações CRUD Avançadas:** Consultas com filtros, uso de projeções e atualizações estruturais (`$set`).
* **Aggregation Pipeline:** Agrupamento de documentos, soma condicional e cálculo de médias integrados nativamente no motor do banco.
* **Otimização e Integridade:** Criação de índices B-Tree (`{ unique: true }`) para bloqueio de duplicações e otimização de consultas (transição de *Collection Scan* para *Index Scan* validada via `explain`).

## 🚀 Como Executar a Camada de Administração (Mongo Express)

No terminal deste ambiente cliente (após configurar a liberação de IP no Security Group da AWS), inicie a interface gráfica via Docker:

```bash
docker run -it --rm \
  -p 8081:8081 \
  -e ME_CONFIG_MONGODB_URL="mongodb://<usuario>:<senha>@<IP_DA_EC2>:27017/?authSource=admin" \
  mongo-express
