# Jim's Codestar Enterprise Pipeline Starwars NodeJS Lambda Microservice

Welcome! I, Jim Lynch, am in the interview process for an awesome position at a really cool startup company where i would potentially be the leader and pioneer of all things serverless! So, I got to thinking: If I were in the position where I was "Head of Serverless" for a company, what would my process look like for developing aws lambda functions _for real?_ What would be the most robust, battle-hardened way of automated testing, automatically deploying (and manual aproval-driven testing for prod), and juggling muliple deployment environments without going crazy? Well, I've found a really nice way to do all this with some awesome AWS services, and I think my ideal dev process would look something like this...


## Try the live api now!

Try hitting the live endpoint via putting it in your browser address bar, ajax, curl, postman, or some other REST client!  

https://ax7ezyq21m.execute-api.us-east-1.amazonaws.com/Prod?character=1


## The Project on The Surface

API that you hit passing in a query parameter, "character", It will then return a json object containing some data about a star wars character: their name, hair cookie, and eye color. The project is written in ES6 nodejs, and is meant to be deployed to aws lambda and run a REST endpoint or scheduled job. 

## The Meta Project
For me, this project was the result of me sitting down and saying, "if I was THE serverless guy for a company, and I needed to create a process for how we should build robust, thoroughly tested, dependable lambda services, how would I do it?". I've used popular CI platforms like Team City, Jenkins, or Travis, but I've found going all-out AWS leads to a nice tighter and simpler integration with your CI pipeline and the actual deploy lambda environment(s).

## Most Reasons Why Serverless is Awsome
I do a lot of front-end javascript development, and honestly I find aws lambda nodejs to be way more fun and interesting. I love how serverless is so small and focused, and I think it just makes it that much easier to have 100% code coverage (to to mention all that view markup to worry about). I love that in serverless development you are quantitatively rewarded for making your code more efficient since you can measure the execution time and max memory used, comparing the numbers over time to find which version of the code works best.

## The CodeStar Dashboard
Codestar Dashboard [here](https://console.aws.amazon.com/codestar/home?region=us-east-1#/projects/jims-cepsnlm/dashboard). 
_(Note: You won't be able to acess the codestar dashboard unless specifically given permissions by Jim.)_

<img src="./images/aws-codestar-dashboard.png" width="650" />

This sample code helps get you started with a simple Express web service
deployed by AWS CloudFormation to AWS Lambda and Amazon API Gateway.

## Why AWS?

Here I'm using AWS CodePipeline, but the Jimbo pipeline is in a way independent of AWS.

## Easy DevOps AWS CodePipeline

<img src="./images/aws-code-pipeline.png" width="650" />

When you make a project with AWS Codestar is automtaically sets up CodePipeline which is a configurable, flexible build, test, and deploy pipeline to which one can add or remove any number of steps. 
I think my ideal pipeline steps would look something like this.

- Commit code to the git repository.
- Code gets automatically picked up by AWS CodePipeline build server.
- Runs Unit tests.
- Run e2e tests
- Generate JsDcoc
- Build project
- Deploy to dev environment
- Run tests against live dev environment
- deploy to staging
- run tests against live staging environment
- manually approve deployment from staging to prod
- deploy to prod


## Unit Tests

The unit tests are meant to test functions in isolation, mocking basically all dependencies.

If you don't have mocha installed globally, please do that first:

`npm i -g mocha`

Then you can run the units tests like so:

`npm test`


Then you can run the test and generate code coverage reports:

`npm test-coverage`

note: in order to run this have you have instabul installed globally:

`npm i -g istanbul`


Notice that right now this template project has 100% test coverage!

<img src="./images/code-coverage-100.png" width="650" />



## E2e Tests

E2e, or "end-to-end" tests can have different meanings in different situations. For front-ends frameworks e2e testing
often involves browser automation, something that doesn't really make sense for a lambda function. In this project I have
two types of e2e tests: 

- rest endpoint e2e tests
- small integration tests

These correspond to the files in the e2e-tests/ folder in the root of this project. They are both run with the command:
`npm run e2e-test`


#### Rest endpoint e2e tests
These tests use the supertest library to hook into the express middleware and basically simulate firing the REST event 
to your function and expecting that the correct response is returned, including headers and authotization-headers.


#### Small Integration Tests
These tests use the supertest library to hook into the express middleware and basically simulate firing the REST event 
to your function and expecting that the correct response is returned, including headers and authotization-headers.
They are similar to unit tests in that they aim to verify the correct return values for individual functions tested in 
isolation. However, unlike unit tests which have side effects such as external requests mocked, these tests allow the functions to call the external apis


## BDD Tests
Bevaior driven development is awsome! But when it comes to the code, what does bdd really mean? In the world of Nodejs it
basically comes to to using CucumberJS to run your "feature files" and "step definition files". Although I haven't yet 
added npm scripts to execute the bdd tests, I have an example feature file that you might use for this project. 
Feature file


## Performance Tests

When it comes to aws lambda functions, you can quantitatively measure the performane of every execution with two numbers: __memory used__ and __duration of function execution__. Measuring the performance of aws lambda functions is actually very easy since every execution of your aws lambda function will output these numbers in the cloudwatch logs (and in the aws lambda console if invoking the function from there).


## Amazon X-ray Performance Analysis 
With each executive of a lambda function you get the total number of milliseconds for which you were billed, but there's no insight into what what going on during that time. Amazon X-ray is a neat service that shows a visual timeline of what's happening during you function execution so you can we how much time the nodejs engine took to start up, how much time each of your functions take to complete, etc. Note that this protect is not currently at up to use aws x-ray, but it would take only a few lives if cute to add it. 

<img src="./images/aws-x-ray-lambda.png" width="650" />


## Included Files for AWS DevOps Pipeline

* buildspec.yml - this file is used by AWS CodeBuild to package your
  service for deployment to AWS Lambda
* template.yml - this file contains the AWS Serverless Application Model (AWS SAM) used
  by AWS CloudFormation to deploy your service to AWS Lambda and Amazon API
  Gateway.


## More AWS Links

Learn more about AWS CodeBuild and how it builds and tests your application here:
https://docs.aws.amazon.com/codebuild/latest/userguide/concepts.html

Learn more about AWS Serverless Application Model (AWS SAM) and how it works here:
https://github.com/awslabs/serverless-application-model/blob/master/HOWTO.md

AWS Lambda Developer Guide:
http://docs.aws.amazon.com/lambda/latest/dg/deploying-lambda-apps.html

Learn more about AWS CodeStar by reading the user guide, and post questions and
comments about AWS CodeStar on our forum.

AWS CodeStar User Guide:
http://docs.aws.amazon.com/codestar/latest/userguide/welcome.html

AWS CodeStar Forum: https://forums.aws.amazon.com/forum.jspa?forumID=248


## Thanks!

Thanks for checking out this repository. Feel free to open issues with questions or suggestions, and if you like this please give it a star!
