# linkpay documentation

### Prerequises

- [Nodejs](https://nodejs.org/) >= 14.x
- [Git](https://git-scm.com/) for versioning
- [gh](https://cli.github.com/) (optional) for github management
- [circleci](https://circleci.com/docs/local-cli/) (optional) for ci/cd pipelines
- [Docker](https://docs.docker.com/get-docker/)
- [Docker-compose](https://docs.docker.com/compose/)

### Databases supported

- [PostreSQL](https://www.prisma.io/docs/concepts/database-connectors/postgresql)
- [Microsoft SQL Server](https://www.prisma.io/docs/concepts/database-connectors/sql-server)
- [Mysql](https://www.prisma.io/docs/concepts/database-connectors/mysql)
- [Sqlite](https://www.prisma.io/docs/concepts/database-connectors/sqlite)
- [MongoDB](https://www.mongodb.com/)

### Documentation

- [Prisma](https://www.prisma.io/docs/reference/api-reference/prisma-schema-reference) For making good schema.
- [Swagger](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.3.md#schemaObject) For making good api's documentation.
- [Supertest](https://www.npmjs.com/package/supertest) For making Api test.
- [Express Js](https://expressjs.com/fr/4x/api.html)

### Run on local

1. Your dev database connection is define in `.env` file
2. Use ``yarn start:stack`` to run all stack the project needs to run (like database)
3. Define your model in **prisma/schema.prisma**
4. Use `yarn update` to update API and database structure following your model in schema.prisma file
5. Use `yarn start:dev` to run project in dev environment
6. Use `yart test` to run tests
7. Use `yarn lint` to lint the code
8. Do something widhfoei iohfo

### Manage versionning (Just at the first launch)

1. Initialize the local repository `git init`
2. Define the main branch `git branch -M main`
3. Add files in `git add .`
4. Commit your code by using `git commit -am "First commit"`
5. Create git repository `gh repo create <%= repo_name %> --source . --remote origin --public --push`
6. If you wnat you open the repository in the browser `gh browse`

### Deploy on gcloud (Cloud run)

1. Build the docker image using `yarn docker:build` (don't forget to change the name of the image as you like)
2. Create your gcloud docker repo `gcloud artifacts repositories create linkpay --location <region></region> --repository-format docker`
3. Get permissions to push image on it using `gcloud auth configure-docker <region>-docker.pkg.dev`
4. Push your docker image by using `docker push <region>-docker.pkg.dev/<project-id>/linkpay/api`
5. Deploy your app on cloud run

   ```bash
   gcloud run deploy linkpay \
    --image=<region>-docker.pkg.dev/<project-id>/linkpay/api \
    --port=80 \
    --min-instances=0 \
    --max-instances=100 \
    --cpu=1 \
    --memory=1024Mi \
    --region=<region> \
    --labels=app=linkpay,env=staging \
    --set-env-vars=""
   ```
