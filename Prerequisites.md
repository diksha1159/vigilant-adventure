Before getting started, you will need the following:

An AWS account

An instance of the AWS Cloud9 (https://aws.amazon.com/cloud9/) IDE or an alternative local compute environment, such as your personal computer
![image](https://user-images.githubusercontent.com/76660222/205568108-acd41a52-6f43-4b7b-bed2-5a30f922ab09.png)


The following installed on your compute environment:

AWS CDK
![image](https://user-images.githubusercontent.com/76660222/205568238-5da7feb9-8e12-49ef-94de-8812003a85bd.png)
https://docs.aws.amazon.com/cloud9/latest/user-guide/sample-cdk.html#sample-cdk-code

AWS Command Line Interface (AWS CLI)
https://aws.amazon.com/cli/
https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html


npm
![image](https://user-images.githubusercontent.com/76660222/205568574-ea58f154-3f9f-4195-a95d-42a209b73914.png)




The AWS Accounts must be bootstrapped for CDK(https://docs.aws.amazon.com/cdk/v2/guide/bootstrapping.html) in the necessary regions. The default configuration uses us-east-1, us-east-2 and us-west-2  as these three regions support CodeArtifact.
![image](https://user-images.githubusercontent.com/76660222/205573420-a053ed4d-2e57-4c92-9893-507941ef99db.png)
![image](https://user-images.githubusercontent.com/76660222/205573512-929832ea-6470-43c7-9639-65dd9b9c3b14.png)


A new AWS Cloud9 IDE is recommended for this tutorial to isolate these actions in this post from your normal compute environment. See the Cloud9 Documentation for Creating an Environment(https://docs.aws.amazon.com/cloud9/latest/user-guide/create-environment-main.html).


