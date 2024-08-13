
```markdown
# Agendamento de Barbearias

Este projeto é uma aplicação para agendamento de barbearias desenvolvida com Next.js. Utiliza uma série de tecnologias e ferramentas modernas para garantir uma aplicação robusta e eficiente. O projeto está configurado para ser executado em um container Docker e suporta autenticação via Google Identity.

## Tecnologias e Ferramentas

- **Next.js**: Framework React para renderização do lado do servidor e criação de aplicações React.
- **Prisma**: ORM (Object-Relational Mapping) para gerenciamento do banco de dados PostgreSQL.
- **Prisma Seed**: Ferramenta para popular o banco de dados com dados iniciais.
- **Husky**: Ferramenta para gerenciar hooks do Git.
- **Sonner**: Biblioteca para notificações e feedbacks visuais.
- **Zod**: Biblioteca para validação de esquemas e tipos.
- **Radix UI**: Conjunto de componentes acessíveis para React.
- **Date-fns**: Biblioteca para manipulação e formatação de datas.
- **PostgreSQL**: Sistema de gerenciamento de banco de dados relacional.
- **Docker**: Plataforma para criação e execução de containers.
- **Google Identity**: Serviço de autenticação para login via Google.

## Pré-requisitos

Antes de começar, você precisará ter as seguintes ferramentas instaladas:

- [Docker](https://www.docker.com/products/docker-desktop) (para execução em containers)
- [Docker Compose](https://docs.docker.com/compose/install/) (para orquestração de múltiplos containers)

## Configuração

### 1. Configuração do Docker

1. **Clone o repositório:**

   ```bash
   git clone https://github.com/seu-usuario/seu-repositorio.git
   cd seu-repositorio
   ```

2. **Crie um arquivo `.env` na raiz do projeto** e adicione as variáveis de ambiente necessárias, incluindo a configuração para o banco de dados PostgreSQL e as credenciais do Google Identity. Exemplo:

   ```env
   DATABASE_URL=postgresql://usuario:senha@db:5432/nome_do_banco
   GOOGLE_CLIENT_ID=seu-google-client-id
   GOOGLE_CLIENT_SECRET=seu-google-client-secret
   ```

3. **Crie o arquivo `docker-compose.yml`** para definir os serviços necessários. Um exemplo básico pode ser:

   ```yaml
   version: '3.8'

   services:
     web:
       image: node:18
       working_dir: /app
       volumes:
         - .:/app
       ports:
         - "3000:3000"
       command: npm run dev
       depends_on:
         - db

     db:
       image: postgres:14
       environment:
         POSTGRES_USER: usuario
         POSTGRES_PASSWORD: senha
         POSTGRES_DB: nome_do_banco
       ports:
         - "5432:5432"

   ```

4. **Inicie os containers:**

   ```bash
   docker-compose up -d
   ```

5. **Configure o Prisma:**

   Execute o comando a seguir para gerar o cliente Prisma e criar o banco de dados:

   ```bash
   docker-compose exec web npx prisma migrate dev --name init
   ```

   Para popular o banco de dados com dados iniciais, use:

   ```bash
   docker-compose exec web npx prisma db seed
   ```

### 2. Configuração do Google Identity

1. **Crie um projeto no [Google Cloud Console](https://console.cloud.google.com/)** e configure a tela de consentimento OAuth.

2. **Crie credenciais OAuth 2.0** e adicione as URLs de redirecionamento apropriadas para o seu ambiente.

3. **Adicione as credenciais ao arquivo `.env`** como mostrado acima.

## Scripts

- **`npm run dev`**: Inicia o servidor de desenvolvimento.
- **`npm run build`**: Compila o projeto para produção.
- **`npm run start`**: Inicia o servidor de produção.
- **`npm run lint`**: Executa o linting para verificar o código.
- **`npm run format`**: Formata o código fonte usando Prettier.

## Contribuição

Se você deseja contribuir para este projeto, por favor, siga estes passos:

1. Faça um fork deste repositório.
2. Crie uma branch para a sua feature (`git checkout -b minha-feature`).
3. Faça commit das suas mudanças (`git commit -am 'Adiciona nova feature'`).
4. Envie a branch para o seu repositório (`git push origin minha-feature`).
5. Abra um Pull Request para o repositório original.

## Licença

Este projeto está licenciado sob a [Licença MIT](LICENSE).

## Contato

Se você tiver alguma dúvida ou sugestão, sinta-se à vontade para abrir uma issue ou entrar em contato diretamente.

---

Obrigado por visitar o projeto de agendamento de barbearias!

```

Este `README.md` fornece uma visão geral completa do projeto, incluindo a configuração para Docker e autenticação via Google Identity. Ajuste as configurações e os exemplos conforme necessário para o seu projeto específico.