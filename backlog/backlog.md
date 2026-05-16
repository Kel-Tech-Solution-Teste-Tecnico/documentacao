# Backlog Técnico - Âmago (Rede Social de Publicações)

**Versão:** 1.0  
**Data:** 16/05/2026  
**Tecnologias:** Flutter (Mobile/Web) | Spring Boot | PostgreSQL | Cloudinary (imagens/vídeos)

---

## TASK001
**Título:** [Backend] Criar modelo de entidade User e repository

**Descrição:**  
**História de usuário:** Como Administrador do sistema, quero persistir dados de usuários para que o cadastro e autenticação funcionem.  
**Requisitos associados:** RF - Cadastro de conta, Login (a partir do diagrama de casos de uso).  
**Critérios de Aceitação:**  
- Entidade User mapeada com campos ID (PK UUID), NAME, EMAIL, PASSWORD, BIO, IMAGE, CREATED_AT, UPDATED_AT.  
- Repository com métodos de CRUD e busca por email.  
- Migração Flyway/Liquibase criada.

**Complementos:**  
- Ver diagrama lógico de banco de dados fornecido.  
- Usar JPA/Hibernate.

**Prioridade:** P0

---

## TASK002
**Título:** [Frontend] Implementar tela de Cadastro de Conta

**Descrição:**  
**História de usuário:** Como Usuário Não Autenticado, quero registrar uma conta para acessar o app.  
**Requisitos associados:** Caso de Uso "Registrar Conta" (diagrama de casos de uso).  
**Critérios de Aceitação:**  
- Formulário com Nome, E-mail, Senha, Confirmar Senha.  
- Validações em tempo real (senhas iguais, email válido).  
- Botão "Cadastrar-se" e link para Login.  
- Integração com endpoint de registro (a ser criado).

**Complementos:**  
- Design conforme imagem "2.png" (tela de cadastro).  
- Usar Flutter com validação de formulário.

**Prioridade:** P0

---

## TASK003
**Título:** [Backend] Implementar endpoint de registro de usuário

**Descrição:**  
**História de usuário:** Como Usuário Não Autenticado, quero registrar uma conta para acessar o app.  
**Requisitos associados:** RF de cadastro (inferido do diagrama).  
**Critérios de Aceitação:**  
- POST /api/auth/register recebe dados e cria usuário.  
- Senha hashed (BCrypt).  
- Validação de email único.  
- Retorna 201 Created ou erros 400/409.

**Complementos:**  
- Referência: imagem de cadastro e modelo USER do BD.

**Prioridade:** P0

---

## TASK004
**Título:** [Frontend] Implementar tela de Login

**Descrição:**  
**História de usuário:** Como Usuário Não Autenticado, quero fazer login para acessar funcionalidades autenticadas.  
**Requisitos associados:** Caso de Uso "Fazer Login".  
**Critérios de Aceitação:**  
- Campos E-mail e Senha.  
- Botão Login e link "Não tem conta? Cadastre-se".  
- Navegação para tela principal após sucesso.  
- Armazenamento seguro de token JWT.

**Complementos:**  
- Design conforme imagem "1.png".

**Prioridade:** P0

---

## TASK005
**Título:** [Backend] Implementar autenticação (Login + JWT)

**Descrição:**  
**História de usuário:** Como Usuário Autenticado, quero me autenticar no sistema.  
**Requisitos associados:** Caso de Uso "Fazer Login".  
**Critérios de Aceitação:**  
- POST /api/auth/login retorna JWT.  
- SecurityConfig com Spring Security.  
- Filtro de autenticação em endpoints protegidos.

**Complementos:**  
- PasswordEncoder + JwtService.

**Prioridade:** P0

---

## TASK006
**Título:** [Frontend] Implementar tela de Perfil do Usuário (Meu Perfil)

**Descrição:**  
**História de usuário:** Como Usuário Autenticado, quero visualizar meu perfil para gerenciar informações pessoais.  
**Requisitos associados:** Caso de Uso "Detalhar Perfil".  
**Critérios de Aceitação:**  
- Exibir foto, nome, bio.  
- Botão "Editar Perfil".  
- Abas: Bilhetes (text), Imagens, Vídeos.  
- Lista de publicações do usuário.

**Complementos:**  
- Design conforme imagens "5.png", "6.png", "4.png" e "8.png".

**Prioridade:** P1

---

## TASK007
**Título:** [Backend] Criar modelo de entidade Post e repository

**Descrição:**  
**História de usuário:** Como Usuário Autenticado, quero publicar conteúdo.  
**Requisitos associados:** Caso de Uso "Cadastrar Post".  
**Critérios de Aceitação:**  
- Entidade Post com ID, USER_ID (FK), TITLE, DESCRIPTION, POST_TYPE (ENUM), FILE, CREATED_AT, UPDATED_AT.  
- Repository com queries por usuário e tipo.

**Complementos:**  
- Ver diagrama lógico USER-POST.

**Prioridade:** P0

---

## TASK008
**Título:** [Frontend] Implementar tela de Nova Publicação

**Descrição:**  
**História de usuário:** Como Usuário Autenticado, quero criar uma nova publicação.  
**Requisitos associados:** Caso de Uso "Cadastrar Post".  
**Critérios de Aceitação:**  
- Upload de arquivo (imagem/vídeo) via Cloudinary.  
- Campos Título e Descrição.  
- Opções Abrir Câmera / Abrir Galeria.  
- Botão Salvar.

**Complementos:**  
- Design conforme imagens "9.png" e "10.png".

**Prioridade:** P1

---

## TASK009
**Título:** [Backend] Implementar endpoint de criação de Post

**Descrição:**  
**História de usuário:** Como Usuário Autenticado, quero criar uma nova publicação.  
**Requisitos associados:** Caso de Uso "Cadastrar Post".  
**Critérios de Aceitação:**  
- POST /api/posts com multipart (arquivo + dados).  
- Upload para Cloudinary.  
- Persistência no banco.  
- Validação de tipo (TEXT/IMAGE/VIDEO).

**Complementos:**  
- Integração Cloudinary SDK.

**Prioridade:** P0

---

## TASK010
**Título:** [Frontend] Implementar feed/listagem de Posts

**Descrição:**  
**História de usuário:** Como Usuário Autenticado, quero listar publicações para visualizar conteúdo.  
**Requisitos associados:** Caso de Uso "Listar Post".  
**Critérios de Aceitação:**  
- Feed com cards de post (imagem/vídeo + texto).  
- Informações de autor e data.  
- Suporte a diferentes tipos de post.

**Complementos:**  
- Design conforme imagem "3.png".

**Prioridade:** P1

---

## TASK011
**Título:** [Backend] Implementar endpoint de listagem de Posts

**Descrição:**  
**História de usuário:** Como Usuário Autenticado, quero listar publicações.  
**Requisitos associados:** Caso de Uso "Listar Post".  
**Critérios de Aceitação:**  
- GET /api/posts (com paginação e filtro por tipo).  
- Endpoint protegido por JWT.

**Complementos:**  
- Query com JOIN para dados do usuário.

**Prioridade:** P1

---

## TASK012
**Título:** [Frontend] Implementar tela de Detalhar Post

**Descrição:**  
**História de usuário:** Como Usuário Autenticado, quero ver detalhes de uma publicação.  
**Requisitos associados:** Caso de Uso "Detalhar Post".  
**Critérios de Aceitação:**  
- Exibição completa do conteúdo.  
- Opções de edição e exclusão (próprio post).

**Complementos:**  
- Modal ou tela dedicada.

**Prioridade:** P2

---

## TASK013
**Título:** [Backend] Implementar endpoint de edição de Post

**Descrição:**  
**História de usuário:** Como Usuário Autenticado, quero editar minhas publicações.  
**Requisitos associados:** Caso de Uso "Editar Post".  
**Critérios de Aceitação:**  
- PUT /api/posts/{id} com validação de ownership.  
- Atualização de título, descrição e arquivo (opcional).

**Complementos:**  
- Design conforme imagem "11.png" (Editar Publicação).

**Prioridade:** P1

---

## TASK014
**Título:** [Frontend] Implementar funcionalidade de Editar Perfil

**Descrição:**  
**História de usuário:** Como Usuário Autenticado, quero editar meu perfil.  
**Requisitos associados:** Caso de Uso "Editar Perfil".  
**Critérios de Aceitação:**  
- Upload de foto de perfil.  
- Edição de Nome e Bio.  
- Botão Salvar.

**Complementos:**  
- Design conforme imagem "7.png".

**Prioridade:** P1

---

## TASK015
**Título:** [Backend] Implementar endpoint de atualização de perfil

**Descrição:**  
**História de usuário:** Como Usuário Autenticado, quero editar meu perfil.  
**Requisitos associados:** Caso de Uso "Editar Perfil".  
**Critérios de Aceitação:**  
- PUT /api/users/profile.  
- Upload de imagem para Cloudinary.

**Complementos:**  
- Atualiza campos NAME, BIO, IMAGE.

**Prioridade:** P1

---

## TASK016
**Título:** [Frontend] Implementar Logout e Apagar Conta

**Descrição:**  
**História de usuário:** Como Usuário Autenticado, quero fazer logout ou apagar minha conta.  
**Requisitos associados:** Casos de Uso "Fazer Logout" e "Apagar Conta".  
**Critérios de Aceitação:**  
- Opções no menu do perfil (conforme imagem "6.png").  
- Confirmação para exclusão.

**Complementos:**  
- Limpeza de token local.

**Prioridade:** P2

---

## TASK017
**Título:** [Backend] Implementar filtro de posts por tipo

**Descrição:**  
**História de usuário:** Como Usuário Autenticado, quero filtrar posts por tipo de arquivo.  
**Requisitos associados:** Caso de Uso "Filtrar Posts por Tipo de Arquivo".  
**Critérios de Aceitação:**  
- Parâmetro type na listagem de posts (TEXT/IMAGE/VIDEO).

**Complementos:**  
- Enum PostType.

**Prioridade:** P2

---

## TASK018
**Título:** [Frontend] Implementar abas de filtro (Bilhetes/Imagens/Vídeos)

**Descrição:**  
**História de usuário:** Como Usuário Autenticado, quero filtrar publicações por tipo no perfil.  
**Requisitos associados:** Caso de Uso "Filtrar Posts por Tipo de Arquivo".  
**Critérios de Aceitação:**  
- Abas funcionais na tela de perfil.

**Complementos:**  
- Conforme imagens de perfil.

**Prioridade:** P2

---

## TASK019
**Título:** [Backend] Implementar exclusão de Post

**Descrição:**  
**História de usuário:** Como Usuário Autenticado, quero apagar minhas publicações.  
**Requisitos associados:** Caso de Uso "Apagar Post".  
**Critérios de Aceitação:**  
- DELETE /api/posts/{id} com verificação de ownership.  
- Remoção lógica ou física + Cloudinary.

**Complementos:**  

**Prioridade:** P1

---

## TASK020
**Título:** [Frontend] Implementar telas de edição/apagar publicação (modais)

**Descrição:**  
**História de usuário:** Como Usuário Autenticado, quero gerenciar minhas publicações.  
**Requisitos associados:** Casos de Uso "Editar Post" e "Apagar Post".  
**Critérios de Aceitação:**  
- Menu de ações (Editar / Apagar) conforme imagem "5.png".

**Complementos:**  

**Prioridade:** P2