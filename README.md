# LetCync – Sistema Inteligente de Registro de Ponto

O LetCync é um sistema de registro de ponto online desenvolvido com foco em simplicidade, robustez e escalabilidade.
Ele combina frontend em React + Material UI, API em PHP com arquitetura MVC, MySQL como banco de dados relacional e integrações com Google Sheets, email e outros serviços externos de auditoria para garantir segurança da informação.

O projeto nasce simples (registro de entrada e saída + consulta de registros), mas foi planejado para evoluir em funcionalidades e robustez, permitindo aplicações empresariais.

🎯 Objetivos do Sistema

Permitir que usuários registrem ponto de entrada e saída de forma rápida e intuitiva.

Fornecer interface moderna e responsiva usando React + Material UI.

Manter registros em banco de dados local (MySQL).

Garantir redundância e segurança espelhando dados em sistemas externos (Google Sheets, email, ou até outro serviço sugerido).

Disponibilizar painel de visualização dos registros.

Servir como base de estudo e crescimento em desenvolvimento full stack.

🏗️ Arquitetura Geral
flowchart TD
    U[Usuário] --> F[Frontend React + Material UI]
    F -->|Axios/Fetch API| A[API PHP MVC]
    A --> B[(MySQL)]
    A --> S[Google Sheets API]
    A --> E[Serviço de Email (SMTP/PHPMailer)]
    B --> P[Painel de Visualização]
    S --> A
    E --> A

Componentes

Frontend:
React + Material UI para interface, formulários de registro e tela de visualização.

Backend (API PHP MVC):
Estrutura MVC organizada para lidar com rotas, validações, lógica de negócios e persistência.

Banco de Dados (MySQL):
Armazena registros oficiais e serve de base para relatórios.

Integrações externas:

Google Sheets (espelhamento de registros para backup/auditoria).

Email (confirmação e alerta de registros).

Futuro: Webhooks, APIs de auditoria, armazenamento em nuvem.

🔑 Funcionalidades Iniciais

Registrar ponto (Entrada / Saída)

Botões distintos para entrada e saída.

Registro automático com data e hora exata.

Campo opcional para observações.

Visualizar registros

Tela com listagem dos pontos batidos.

Sincronização em tempo real com backend.

Opção de filtros por data/usuário.

Integrações

Backup em Google Sheets.

Envio de email para o próprio usuário ou gestor.

🛠️ Tecnologias Utilizadas
Frontend

React 18+

Material UI (MUI v5)

Axios (requisições HTTP)

Day.js (manipulação de datas)

Backend (API MVC em PHP)

PHP 8+

Composer (dependências)

PHPMailer (envio de emails)

Google API Client (Sheets)

Banco de Dados

MySQL 8+ (produção)

SQLite (para estudo/local)

⚙️ Estrutura do Projeto
1. Backend (PHP MVC)
backend/
 ├── app/
 │    ├── Controllers/
 │    │     ├── RegistroController.php
 │    ├── Models/
 │    │     ├── Registro.php
 │    ├── Views/
 │    │     ├── api_responses/
 │    ├── Core/
 │    │     ├── Database.php
 │    │     ├── Router.php
 │    │     ├── Controller.php
 │    │     ├── Model.php
 │    └── Helpers/
 │          ├── EmailHelper.php
 │          ├── SheetsHelper.php
 ├── public/
 │     └── index.php
 ├── config/
 │     ├── config.php
 │     ├── database.php
 ├── vendor/
 └── composer.json

2. Frontend (React + MUI)
frontend/
 ├── src/
 │    ├── components/
 │    │     ├── RegistroButton.js
 │    │     ├── RegistroList.js
 │    ├── pages/
 │    │     ├── Home.js
 │    │     ├── Registros.js
 │    ├── services/
 │    │     ├── api.js
 │    ├── utils/
 │    │     ├── formatDate.js
 │    ├── App.js
 │    ├── index.js
 ├── package.json
 └── public/

📂 Banco de Dados
Tabela: registros
CREATE TABLE registros (
    id INT AUTO_INCREMENT PRIMARY KEY,
    usuario VARCHAR(100) NOT NULL,
    tipo ENUM('entrada','saida') NOT NULL,
    observacao TEXT,
    data_hora TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

📬 Integrações
Google Sheets

Criar planilha de backup.

Configurar credenciais via Google Cloud.

Espelhar cada registro.

Email (SMTP / PHPMailer)

Enviar notificação a cada ponto batido.

Configurável para enviar cópia a gestores.

🔒 Segurança da Informação

Todos os acessos à API devem ser feitos via HTTPS.

Backend em PHP deve implementar validação de entrada e filtros contra SQL Injection.

Futuro: autenticação com JWT (JSON Web Tokens) para identificar usuários.

Redundância: MySQL (principal) + Google Sheets (espelho).

🚀 Roadmap de Evolução

MVP – Registro simples (Entrada/Saída) + listagem + backup Sheets + email.

Fase 2 – Login de usuários e relatórios básicos.

Fase 3 – Dashboard de métricas (React Charts).

Fase 4 – Exportação de relatórios (Excel/PDF).

Fase 5 – Integração mobile (React Native ou PWA).

Fase 6 – Notificações via WhatsApp/Telegram.

Fase 7 – Machine Learning (detectar padrões de ponto, anomalias).

📚 Guia de Estudo (sugestão para você evoluir)

Entender a arquitetura MVC no PHP.

Criar a API RESTful com rotas básicas (/registrar, /listar).

Conectar ao MySQL e salvar registros.

Integrar com Google Sheets API.

Adicionar PHPMailer para envio de emails.

Criar frontend React + Material UI.

Conectar frontend com API via Axios.

Criar tela de listagem de registros.

Evoluir com autenticação, relatórios e dashboards.
