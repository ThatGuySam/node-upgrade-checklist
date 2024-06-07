# Node Upgrade Checklist
Handy checklist for everywhere and anywhere you might need to set the version when upgrading to the latest Node. 


[Fixes and Updates Welcome](https://github.com/ThatGuySam/node-upgrade-checklist/edit/main/README.md)


Here's the comprehensive list with code examples, using Node version 22 as the example:

### **`package.json` Engines**
```JavaScript
// package.json
{
  "engines": {
    "node": "22.x"
  }
}
// https://docs.npmjs.com/cli/configuring-npm/package-json#engines
```

### **`.nvmrc`**
```
// .nvmrc
22
// https://github.com/nvm-sh/nvm#nvmrc
```

### **`.node-version`**
```
// .node-version
22
// https://github.com/shadowspawn/node-version-usage
```

### **`.npmrc`**
```
// .npmrc
use-node-version=22
// https://docs.npmjs.com/cli/configuring-npm/npmrc
```

### **GitHub Actions**
```yaml
# .github/workflows/ci.yml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          # https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-nodejs#specifying-the-nodejs-versionz
          node-version: '22'
```

### **Dependency Managers**
Reminder: Run `npm install`, `pnpm install`, etc... after updating the Node version to ensure dependencies are compatible.

### **Vercel Build and Serverless Config**
⭐️ Defaults to Node Version in package.json/engines
https://vercel.com/docs/project-configuration#project-configuration/build
[Available Node Versions](https://vercel.com/docs/functions/runtimes/node-js#default-and-available-versions)

### **Netlify Build Config**
⭐️ Setting .node-version or .nvmrc will override the version set in the Netlify UI. 
```toml
# netlify.toml
[context.production]
  environment = { NODE_VERSION = "22.0.0" }
# https://docs.netlify.com/configure-builds/manage-dependencies/#node-js-and-javascript
```
[Netlify TOML file reference](https://docs.netlify.com/configure-builds/file-based-configuration/)


### **Netlify Runtime/Serverless Config**
Unfortunately, as of June 2024 this can only be set in the Netlify UI. 
```bash
AWS_LAMBDA_JS_RUNTIME=nodejs22.x
```
[Netlify Runtime Node Version](https://docs.netlify.com/functions/optional-configuration/?fn-language=js#node-js-version-for-runtime-2)
[Support Lambda Versions](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html#w364aac19c29)


### **Update `@types/node`**
```bash
npm install --save-dev @types/node@22
pnpm add --dev @types/node@22
# https://www.npmjs.com/package/@types/node
```

### **AWS Lambda**
AWS Lambda uses the `runtime` parameter in the function configuration. Update it via the AWS Management Console or AWS CLI.

- AWS Console: [Link to Console](https://console.aws.amazon.com/lambda/home)
- AWS CLI:
```bash
aws lambda update-function-configuration --function-name my-function --runtime nodejs22.x
# https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html
```
[Support Lambda Versions](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html#w364aac19c29)

### **Dockerfile**
```dockerfile
# Dockerfile
FROM node:22
# https://docs.docker.com/samples/node/
```

### **Heroku**
To specify the version of Node.js to use on Heroku, use the engines section of the package.json. Drop the v to save only the version number.
[Heroku Node.js Version](https://devcenter.heroku.com/articles/nodejs-support#specifying-a-node-js-version)

### **CircleCI**
```yaml
# .circleci/config.yml
version: 2.1
jobs:
  build:
    docker:
      - image: circleci/node@5
    steps:
      - checkout
      - node/install:
          node-version: '22'
```
[CircleCI Node.js Version](https://circleci.com/docs/language-javascript/)

### **TravisCI**
⭐️ If you don't specify a Node version, Travis CI will use the default to the version set in `.nvmrc`
```yaml
# .travis.yml
language: node_js
node_js:
  - "22"
```
[TravisCI Node.js Version](https://docs.travis-ci.com/user/languages/javascript-with-nodejs/)

### **AWS Elastic Beanstalk**
Update the Node version in the `platform` configuration via the AWS Management Console or CLI.

- AWS Console: [Link to Console](https://console.aws.amazon.com/elasticbeanstalk/home)
- AWS CLI:
```bash
aws elasticbeanstalk update-environment --environment-name my-env --option-settings Namespace=aws:elasticbeanstalk:container:nodejs,OptionName=NodeVersion,Value=22
# https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/platforms-linux.html#platforms-linux.nodejs
```

### **Google Cloud Functions**
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
