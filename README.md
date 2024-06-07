# Node Upgrade Checklist
Handy checklist for upgrading to the latest Node Version


Here's the comprehensive list with code examples, using Node version 22 as the example:

### 1. **`package.json` Engines**
```json
// package.json
{
  "engines": {
    "node": ">=22.0.0"
  }
}
// https://docs.npmjs.com/files/package.json#engines
```

### 2. **`.nvmrc`**
```
// .nvmrc
22.0.0
// https://github.com/nvm-sh/nvm#nvmrc
```

### 3. **`.node-version`**
```
// .node-version
22.0.0
// https://github.com/nodenv/nodenv#node-version
```

### 4. **`.npmrc`**
```
// .npmrc
use-node-version=22.0.0
// https://docs.npmjs.com/cli/v7/configuring-npm/npmrc
```

### 5. **Dependency Managers**
Reminder: Run `npm install` or `yarn install` after updating the Node version to ensure dependencies are compatible.

### 6. **GitHub Actions**
```yaml
# .github/workflows/ci.yml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '22'
      # https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-nodejs
```

### 7. **Vercel Config**
```json
// vercel.json
{
  "build": {
    "env": {
      "NODE_VERSION": "22"
    }
  }
}
// https://vercel.com/docs/project-configuration#project-configuration/build
```

### 8. **Netlify Config**
```toml
# netlify.toml
[build.environment]
  NODE_VERSION = "22"
# https://docs.netlify.com/configure-builds/manage-dependencies/#node-js-and-javascript
```

### 9. **Update `@types/node`**
```bash
npm install --save-dev @types/node@22
# or
yarn add --dev @types/node@22
# https://www.npmjs.com/package/@types/node
```

### 10. **AWS Lambda**
AWS Lambda uses the `runtime` parameter in the function configuration. Update it via the AWS Management Console or AWS CLI.

- AWS Console: [Link to Console](https://console.aws.amazon.com/lambda/home)
- AWS CLI:
```bash
aws lambda update-function-configuration --function-name my-function --runtime nodejs22.x
# https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html
```

### 11. **Netlify Function Runtime ENV Variable**
```toml
# netlify.toml
[functions.environment]
  NODE_VERSION = "22"
# https://docs.netlify.com/functions/optional-configuration/?fn-language=ts#node-js-version-for-runtime
```

### 12. **Dockerfile**
```dockerfile
# Dockerfile
FROM node:22
# https://docs.docker.com/samples/node/
```

### 13. **Heroku**
- Set `engines.node` in `package.json` as shown in item 1.
- Set `NODE_VERSION` environment variable via the Heroku Dashboard or CLI.

- Heroku Dashboard: [Link to Dashboard](https://dashboard.heroku.com/)
- Heroku CLI:
```bash
heroku config:set NODE_VERSION=22
# https://devcenter.heroku.com/articles/nodejs-support#specifying-a-node-js-version
```

### 14. **CircleCI**
```yaml
# .circleci/config.yml
version: 2.1
jobs:
  build:
    docker:
      - image: circleci/node:22
    steps:
      - checkout
      - run: npm install
# https://circleci.com/docs/2.0/language-javascript/
```

### 15. **TravisCI**
```yaml
# .travis.yml
language: node_js
node_js:
  - "22"
# https://docs.travis-ci.com/user/languages/javascript-with-nodejs/
```

### 16. **AWS Elastic Beanstalk**
Update the Node version in the `platform` configuration via the AWS Management Console or CLI.

- AWS Console: [Link to Console](https://console.aws.amazon.com/elasticbeanstalk/home)
- AWS CLI:
```bash
aws elasticbeanstalk update-environment --environment-name my-env --option-settings Namespace=aws:elasticbeanstalk:container:nodejs,OptionName=NodeVersion,Value=22
# https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/platforms-linux.html#platforms-linux.nodejs
```

### 17. **Google Cloud Functions**
Set `engines.node` in `package.json` as shown in item 1.

- Google Cloud Console: [Link to Console](https://console.cloud.google.com/functions/)
- Google Cloud CLI:
```bash
gcloud functions deploy my-function --runtime nodejs22
# https://cloud.google.com/functions/docs/concepts/nodejs-runtime
```

### Summary Output
Ensure the CLI tool provides an output summary of all changes made, listing the files and their updated values. This helps in verifying the updates and troubleshooting any issues.

By following this comprehensive checklist and utilizing the code examples, you can ensure a smooth transition to a new Node version across various environments and configurations.
