# smithy-typescript-template-lambda-service
A Smithy Typescript service hosted on AWS Lambda.

# Overview

This repository is divided into three projects:

- `model` contains the Smithy model for the service.
- `typescript-client` contains the generated TypeScript client generated from `model`.
- `server` contains the service, written in TypeScript, for `model`.

# Building

## Prerequisites

Before beginning:
- Install
    - [JDK](https://aws.amazon.com/corretto/) >= 8
    - [NodeJS](https://nodejs.org/en/download/) >= 14
    - [Yarn](https://yarnpkg.com/getting-started/install) >= 2
    - [Docker](https://docs.docker.com/get-docker/) 
- Set up an [AWS account](https://portal.aws.amazon.com/billing/signup) if you do not have one
- [Configure your workstation](https://docs.aws.amazon.com/cdk/latest/guide/getting_started.html#getting_started_prerequisites)
  so the CDK can use your account

## Getting started

1. After the first checkout, you will need to kick off the initial code generation by running:
    ```bash
    cd model
    ./gradlew build pTML
    cd ../typescript-client/codegen
    ./gradlew clean build
    cd ../../server/codegen
    ./gradlew clean build
    cd ../../
    ```
2. Next, run `yarn install && yarn build` to do the initial build of the entire project.
3. To deploy the service, run `cd server && yarn cdk deploy`. When complete, the CDK will print out the endpoint URL
   for your newly deployed service.
   >   Note: this step will create resources in your AWS account that may incur charges.
4. To test your service, switch to the `typescript-client` directory and use `yarn str-length` to call the `Length`
   operation. For example, given an output from the CDK of 
   `https://somerandomstring.execute-api.us-west-2.amazonaws.com/prod/`,
   ```bash
   yarn str-length https://somerandomstring.execute-api.us-west-2.amazonaws.com/prod/ foobar
   ```
   should print out `6`.
