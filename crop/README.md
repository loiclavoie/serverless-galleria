# crop

Copy and crop images using Lambda.

## Deploy with CloudFormation

Prerequisites: [Node.js](https://nodejs.org/en/) and [AWS CLI](http://docs.aws.amazon.com/cli/latest/userguide/installing.html) installed

* Create an [AWS](https://aws.amazon.com/) Account and [IAM User](https://aws.amazon.com/iam/) with the `AdministratorAccess` AWS [Managed Policy](http://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html)
* Run `aws configure` to put store that user's credentials in `~/.aws/credentials`
* Create an S3 bucket for storing the Lambda code and store its name in a shell variable with:
  * `export CODE_BUCKET=bucket`
* Create the S3 bucket for the cropped output, store its name in shell variable:
  * `export DEST_BUCKET=bucket`
* Choose a name, but do NOT create the S3 bucket input comes from, store its name in shell variable:
  * `export SOURCE_BUCKET=bucket`
* Choose the width in pixels, store it in shell variable:
  * `export WIDTH=600`
* Choose the height in pixels, store it in shell variable:
  * `export HEIGHT=400`
* Choose the x in pixels (number of pixels right from left edge to remove), store it in shell variable:
  * `export X=50`
* Choose the y in pixels (number of pixels down from the top to remove), store it in shell variable:
  * `export Y=50`
* Npm install:
  * `npm install`
* Build:
  * `npm run build`
* Upload package to S3, transform the CloudFormation template:
  * Unix: `npm run package`
  * Windows : `aws cloudformation package --template-file template.yml --output-template-file packaged-template.yml --s3-bucket $CODE_BUCKET`
* Deploy to CloudFormation:
  * Unix: `npm run deploy`
  * Windows: `aws cloudformation deploy --template-file packaged-template.yml --capabilities CAPABILITY_IAM --stack-name dev-crop-project --parameter-overrides sourceBucket=$SOURCE_BUCKET destBucket=$DEST_BUCKET mode=CENTERED width=$WIDTH height=$HEIGHT xCoordinate=$X yCoordinate=$Y`

## Deploy from the AWS Serverless Application Repository
* Create the destination bucket
* Hit "Deploy" from the [application](https://serverlessrepo.aws.amazon.com/#/applications/arn:aws:serverlessrepo:us-east-1:233054207705:applications~crop) page

## Use
* Images that you put into the source bucket will be transformed, then put into the destination bucket

## Links
* [serverless-galleria](https://github.com/evanchiu/serverless-galleria) on Github
* [crop](https://serverlessrepo.aws.amazon.com/#/applications/arn:aws:serverlessrepo:us-east-1:233054207705:applications~crop) on the AWS Serverless Application Repository

## License
&copy; 2017-2019 [Evan Chiu](https://evanchiu.com). This project is available under the terms of the MIT license.
