# PRD - Sistema de Processamento e Gestão Documental Automatizado (DocProcess)

**Versão:** 1.0  
**Data:** 16/05/2026  
**Tecnologias:** Flutter (Web, Android, iOS) | Spring Boot | PostgreSQL | Cloudinary

## Mini-mundo

A empresa de gestão documental recebe documentos digitalizados (PDF e PNG) dos clientes. O Operador realiza o upload dos arquivos, que são armazenados no **Cloudinary**. O sistema processa automaticamente cada documento (extração de texto, OCR e identificação de padrões: data_texto, valor_monetario, cpf, cnpj), gera um XML estruturado e atualiza o status. O Operador acompanha o status e corrige eventuais erros. O Gestor consulta e filtra relatórios consolidados. O Administrador gerencia clientes e acompanha o histórico de logs. O objetivo é automatizar todo o processamento manual e entregar XMLs confiáveis como saída principal.

## Requisitos Funcionais

**RF001**  
**Caso de Uso:** Fazer Upload de Arquivo  
**Descrição:** Permite ao Operador realizar upload individual ou em lote de documentos PDF/PNG. O arquivo é enviado para o Cloudinary e um registro é criado no sistema.  
**Atores:** Operador  
**Requisito de Dependência:** Nenhum  

**Dados de Entrada:**

| Nome           | Tipo de Dado      | Obrigatório | Propriedade/Regra                  |
|----------------|-------------------|-------------|------------------------------------|
| arquivos      | Multipart File[] | S           | PDF ou PNG, 2MB a 25MB             |
| clienteId     | UUID              | S           | Cliente deve existir               |

**Dados de Saída:**

| Nome           | Tipo de Dado      | Obrigatório | Propriedade/Regra                     |
|----------------|-------------------|-------------|---------------------------------------|
| documentoIds  | List<UUID>        | S           | IDs dos documentos criados            |
| status        | String            | S           | "Recebido"                            |

**RF002**  
**Caso de Uso:** Acompanhar Status de Processamento  
**Descrição:** Operador consulta o status atual dos documentos enviados (Recebido, Processando, Processado, XML_Gerado, Erro).  
**Atores:** Operador  
**Requisito de Dependência:** RF001  

**RF003**  
**Caso de Uso:** Corrigir Erros  
**Descrição:** Operador visualiza os dados extraídos e realiza correções manuais em documentos com erro ou status Processado.  
**Atores:** Operador  
**Requisito de Dependência:** RF001, RF002  

**RF004**  
**Caso de Uso:** Consultar Relatórios  
**Descrição:** Gestor visualiza relatórios consolidados de documentos processados e XMLs gerados.  
**Atores:** Gestor  
**Requisito de Dependência:** RF001, RF002, RF003  

**RF005**  
**Caso de Uso:** Filtrar Relatórios Por Período  
**Descrição:** Gestor filtra relatórios por intervalo de datas.  
**Atores:** Gestor  
**Requisito de Dependência:** RF004  

**RF006**  
**Caso de Uso:** Filtrar Relatórios Por Data  
**Descrição:** Gestor filtra relatórios por uma data específica.  
**Atores:** Gestor  
**Requisito de Dependência:** RF004  

**RF007**  
**Caso de Uso:** Filtrar Relatórios Por Tipo de Documento  
**Descrição:** Gestor filtra relatórios por tipo (PDF ou PNG).  
**Atores:** Gestor  
**Requisito de Dependência:** RF004  

**RF008**  
**Caso de Uso:** Filtrar Relatórios Por Cliente  
**Descrição:** Gestor filtra relatórios por cliente.  
**Atores:** Gestor  
**Requisito de Dependência:** RF004  

**RF009**  
**Caso de Uso:** Criar Clientes  
**Descrição:** Administrador realiza o cadastro de novos clientes.  
**Atores:** Administrador  
**Requisito de Dependência:** Nenhum  

**RF010**  
**Caso de Uso:** Acompanhar Histórico de Logs  
**Descrição:** Administrador consulta o histórico completo de logs e auditoria do sistema.  
**Atores:** Administrador  
**Requisito de Dependência:** Nenhum  

## Endpoints (API - Spring Boot)

- **POST** `/api/documentos/upload` → RF001  
- **GET** `/api/documentos` → Listagem com status (RF002)  
- **GET** `/api/documentos/{id}` → Detalhes do documento  
- **PUT** `/api/documentos/{id}/corrigir` → RF003  
- **GET** `/api/relatorios` → RF004  
- **GET** `/api/relatorios/periodo` → RF005  
- **GET** `/api/relatorios/data` → RF006  
- **GET** `/api/relatorios/tipo` → RF007  
- **GET** `/api/relatorios/cliente` → RF008  
- **POST** `/api/clientes` → RF009  
- **GET** `/api/logs` → RF010  
- **GET** `/api/documentos/{id}/xml/download` → Download do XML

## Requisitos Não Funcionais

**RNF001**  
**Descrição:** Processamento completo em até 30 segundos por documento.  
**Categoria:** Desempenho

**RNF002**  
**Descrição:** Suportar até 5.000 documentos/dia e 100 usuários simultâneos.  
**Categoria:** Escalabilidade / Capacidade

**RNF003**  
**Descrição:** Criptografia de dados sensíveis (CPF, CNPJ, valores monetários).  
**Categoria:** Segurança

**RNF004**  
**Descrição:** Interface responsiva em Flutter (Web, Android e iOS).  
**Categoria:** Usabilidade

**RNF005**  
**Descrição:** Logs estruturados em JSON para todas as operações.  
**Categoria:** Manutenibilidade

**RNF006**  
**Descrição:** Disponibilidade mínima de 99%.  
**Categoria:** Disponibilidade

## Regras de Negócio

**RN001**  
**Descrição:** Apenas arquivos PDF e PNG entre 2MB e 25MB são aceitos.  
**Dependência:** -

**RN002**  
**Descrição:** O XML só é gerado após o processamento bem-sucedido.  
**Dependência:** RN001

**RN003**  
**Descrição:** Campos extraídos devem ser validados por regex antes da geração do XML.  
**Dependência:** -

**RN004**  
**Descrição:** Arquivos brutos são mantidos no Cloudinary por 90 dias.  
**Dependência:** -

## Diagrama de Caso de Uso

```mermaid
flowchart TD
    subgraph Sistema["DocProcess System"]
        UC1["Fazer Upload de Arquivo"]
        UC2["Acompanhar Status de Processamento"]
        UC3["Corrigir Erros"]
        UC4["Consultar Relatórios"]
        UC5["Filtrar Relatórios Por Período"]
        UC6["Filtrar Relatórios Por Data"]
        UC7["Filtrar Relatórios Por Tipo de Documento"]
        UC8["Filtrar Relatórios Por Cliente"]
        UC9["Criar Clientes"]
        UC10["Acompanhar Histórico de Logs"]
    end

    Operador["🎭 Operador"] --> UC1
    Operador --> UC2
    Operador --> UC3

    Gestor["🎭 Gestor"] --> UC4
    Gestor --> UC5
    Gestor --> UC6
    Gestor --> UC7
    Gestor --> UC8

    Administrador["🎭 Administrador"] --> UC9
    Administrador --> UC10

    UC1 -.-> UC2
    UC2 -.-> UC3


# Modelo Lógico de Banco de Dados

## Tabela: `clientes`

| Campo | Tipo | Restrições |
|-------|------|------------|
| id | UUID | PK |
| nome | VARCHAR(255) | NOT NULL |
| cnpj | VARCHAR(18) | UNIQUE, NOT NULL |
| data_cadastro | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP |

---

## Tabela: `usuarios`

| Campo | Tipo | Restrições |
|-------|------|------------|
| id | UUID | PK |
| nome | VARCHAR(255) | NOT NULL |
| email | VARCHAR(255) | UNIQUE, NOT NULL |
| senha_hash | VARCHAR(255) | NOT NULL |
| role | ENUM('OPERADOR', 'GESTOR', 'ADMINISTRADOR') | NOT NULL |
| ativo | BOOLEAN | DEFAULT true |

---

## Tabela: `documentos`

| Campo | Tipo | Restrições |
|-------|------|------------|
| id | UUID | PK |
| cliente_id | UUID | FK |
| operador_id | UUID | FK |
| nome_arquivo_original | VARCHAR(500) | NOT NULL |
| cloudinary_public_id | VARCHAR(255) | UNIQUE, NOT NULL |
| cloudinary_url | VARCHAR(1000) | NOT NULL |
| cloudinary_secure_url | VARCHAR(1000) | NOT NULL |
| tipo_arquivo | ENUM('PDF', 'PNG') | NOT NULL |
| tamanho_bytes | BIGINT | NOT NULL |
| texto_extraido | TEXT | |
| dados_extraidos | JSONB | |
| status | ENUM('Recebido', 'Processando', 'Processado', 'XML_Gerado', 'Erro') | NOT NULL, DEFAULT 'Recebido' |
| data_upload | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP |
| data_processamento | TIMESTAMP | |

---

## Tabela: `xml_gerados`

| Campo | Tipo | Restrições |
|-------|------|------------|
| id | UUID | PK |
| documento_id | UUID | UNIQUE, FK |
| conteudo_xml | TEXT | NOT NULL |
| cloudinary_public_id_xml | VARCHAR(255) | |
| cloudinary_url_xml | VARCHAR(1000) | |
| data_geracao | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP |

---

## Tabela: `logs_auditoria`

| Campo | Tipo | Restrições |
|-------|------|------------|
| id | UUID | PK |
| usuario_id | UUID | FK |
| documento_id | UUID | FK, NULL |
| acao | VARCHAR(100) | NOT NULL |
| descricao | TEXT | |
| data_hora | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP |

---

# Relacionamentos

```text
[clientes]     (1,1) ────── (0,n) [documentos]
[usuarios]     (1,1) ────── (0,n) [documentos]
[documentos]   (1,1) ────── (0,1) [xml_gerados]
```

---

# Possível Fluxo de Telas (Flutter)

## Autenticação
- Tela de Login

## Operador
- Dashboard (resumo quantitativo)
- Tela de Upload
- Lista de Documentos com Status
- Detalhes do Documento + Correção

## Gestor
- Relatórios com múltiplos filtros

## Administrador
- Cadastro de Clientes
- Histórico de Logs

---

# Cenários de Testes de Software

## RF001 - Fazer Upload de Arquivo

| ID | Requisito | Cenário | Descrição | Entrada | Resultado Esperado |
|----|------------|---------|------------|---------|---------------------|
| TEST-RF001-S1 | RF001 | Sucesso | Upload válido | PDF 10MB + clienteId válido | `201 Created` + `documentoId` |
| TEST-RF001-F1 | RF001 | Falha | Tamanho excedido | Arquivo 30MB | `400 Bad Request` + `"Tamanho máximo 25MB"` |
| TEST-RF001-F2 | RF001 | Falha | Tipo inválido | Arquivo `.exe` | `400 Bad Request` + `"Apenas PDF e PNG permitidos"` |
| TEST-RF001-F3 | RF001 | Falha | Cliente inexistente | clienteId inválido | `404 Not Found` |

> Os demais requisitos seguem o mesmo padrão: **1 cenário de sucesso + 3 cenários de falha**.