Before getting started, you will need the following:

An AWS account

An instance of the AWS Cloud9 (https://aws.amazon.com/cloud9/) IDE or an alternative local compute environment, such as your personal computer


The following installed on your compute environment:

AWS CDK

AWS Command Line Interface (AWS CLI)
https://aws.amazon.com/cli/


npm


The AWS Accounts must be bootstrapped for CDK(https://docs.aws.amazon.com/cdk/v2/guide/bootstrapping.html) in the necessary regions. The default configuration uses us-east-1, us-east-2 and us-west-2  as these three regions support CodeArtifact.
A new AWS Cloud9 IDE is recommended for this tutorial to isolate these actions in this post from your normal compute environment. See the Cloud9 Documentation for Creating an Environment(https://docs.aws.amazon.com/cloud9/latest/user-guide/create-environment-main.html).
