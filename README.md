#  LetCync – Sistema Inteligente de Registro de Ponto
📖 Visão Geral

O LetCync é um sistema de registro de ponto online, moderno, seguro e escalável, desenvolvido para empresas e estudos pessoais de desenvolvimento.
Ele combina:

Frontend: React + Material UI

Backend: PHP (API RESTful MVC)

Banco de Dados: MySQL

Integrações: Google Sheets (backup), Email (PHPMailer)

Autenticação e autorização: cadastro de usuários e perfis de acesso

O objetivo é permitir que cada usuário registre seus próprios pontos com controle de acesso, mantendo auditoria e segurança da informação.

🎯 Objetivos do Sistema

Permitir que usuários registrem ponto de entrada e saída de forma segura.

Evitar que alguém bata ponto por outro.

Diferenciar perfis de acesso:

Usuário comum → vê apenas seus pontos.

Administrador → vê pontos de todos os usuários.

Manter histórico seguro em MySQL e Google Sheets.

Notificar por email cada registro.

Servir como base para estudo full-stack e evolução do sistema.

🏗️ Arquitetura Geral
flowchart TD
    U[Usuário] -->|Login| F[Frontend React + Material UI]
    F -->|API REST (Axios)| A[Backend PHP MVC]
    A --> B[(MySQL)]
    A --> S[Google Sheets API]
    A --> E[Serviço de Email (SMTP/PHPMailer)]
    B --> P[Painel de Visualização]
    S --> A
    E --> A

🔑 Funcionalidades
1. Cadastro e Login de Usuário

Cadastro com nome, email e senha.

Login seguro com hash de senha (bcrypt).

Perfis:

user → acesso ao próprio ponto

admin → acesso a todos os pontos

Sessão JWT ou PHP Session para manter autenticação segura.

2. Registro de Ponto

Entrada e saída com data/hora automática.

Campo opcional de observações (ex: home office).

Sincronização com Google Sheets e MySQL.

Email de confirmação para o usuário.

3. Visualização de Registros

Usuário comum → somente seus registros.

Administrador → todos os registros da empresa.

Filtro por data e usuário (para admins).

Dashboard opcional para relatórios visuais.

4. Segurança

HTTPS obrigatório.

Hash de senha no banco.

Controle de sessão via JWT ou PHP Session.

Validação de input para evitar SQL Injection.

Redundância: MySQL + Google Sheets.

🛠️ Tecnologias Utilizadas
Frontend

React 18+

Material UI (MUI v5)

Axios (API REST)

Day.js (datas)

Backend

PHP 8+

Composer

PHPMailer

Google API Client (Sheets)

Banco de Dados

MySQL (produção)

SQLite (local/estudo)

⚙️ Estrutura do Projeto
Backend (PHP MVC)
backend/
 ├── app/
 │    ├── Controllers/
 │    │     ├── AuthController.php    # login, registro
 │    │     ├── RegistroController.php
 │    ├── Models/
 │    │     ├── User.php
 │    │     ├── Registro.php
 │    ├── Views/
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

Frontend (React + MUI)
frontend/
 ├── src/
 │    ├── components/
 │    │     ├── RegistroButton.js
 │    │     ├── RegistroList.js
 │    │     ├── LoginForm.js
 │    │     ├── RegisterForm.js
 │    ├── pages/
 │    │     ├── Home.js
 │    │     ├── Registros.js
 │    │     ├── Login.js
 │    │     ├── Register.js
 │    ├── services/
 │    │     ├── api.js
 │    ├── utils/
 │    │     ├── auth.js
 │    │     ├── formatDate.js
 │    ├── App.js
 │    ├── index.js
 ├── package.json
 └── public/

📂 Banco de Dados
Tabela: users
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(150) NOT NULL UNIQUE,
    senha VARCHAR(255) NOT NULL,
    perfil ENUM('user','admin') DEFAULT 'user',
    criado_em TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

Tabela: registros
CREATE TABLE registros (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    tipo ENUM('entrada','saida') NOT NULL,
    observacao TEXT,
    data_hora TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id)
);

📬 Integrações
Google Sheets

Criação de backup para redundância.

API via Google Service Account.

Email (PHPMailer)

Confirmação de ponto registrado para usuário.

Notificação opcional para admin.

Futuro

Webhook ou outro sistema de auditoria.

Painel gráfico de métricas.

🚀 Roadmap

MVP: cadastro/login, registro de ponto, visualização pessoal, Google Sheets, email.

Autenticação JWT ou PHP Session robusta.

Dashboard para admins.

Relatórios, exportações PDF/Excel.

Mobile PWA.

Notificações externas (WhatsApp/Telegram).

ML para detecção de anomalias de ponto.

🔒 Segurança

HTTPS.

Hash bcrypt nas senhas.

Validação de input.

Perfis de acesso (user, admin).

Backup de dados e redundância.
