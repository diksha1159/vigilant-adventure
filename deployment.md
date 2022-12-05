# Deployment instructions:

Deploy the Python Package Publishing Pipeline into your AWS Account with the CDK

The source code can be found in this GitHub Repository (https://github.com/aws-samples/multi-region-python-package-publishing-pipeline) .

Fork the GitHub Repo into your account. This way you can experiment with changes as necessary to fit your workload.
In your local compute environment, clone the GitHub Repository and cd into the project directory:

    git clone git@github.com:<YOUR_GITHUB_USERNAME>/multi-region-
      python-package-publishing-pipeline.git && cd multi-region-
      python-package-publishing-pipeline

![image](https://user-images.githubusercontent.com/76660222/205576542-dc56c7ba-c499-4785-a7d3-b582c72f1c11.png)

Install the necessary node packages:

    npm i

![image](https://user-images.githubusercontent.com/76660222/205577117-dd19a5f4-71a8-4bde-b7a5-a2b25e2088ba.png)

## Deploy the CDK Application
 `cdk deploy --all` from the app root directory `multi-region-python-package-publishing-pipeline/`* Enter `y` for all prompts
 ![image](https://user-images.githubusercontent.com/76660222/205584131-878821b7-6294-44bb-af68-e82f286fdc3e.png)
![image](https://user-images.githubusercontent.com/76660222/205584204-fca7526b-ecc1-4d01-a0a2-0189c95e1ac8.png)


## Viewing the deployed CloudFormation stacks

After the deployment of the AWS CDK application completes, you can view the deployed AWS CDK Stacks via CloudFormation. 
From the [AWS Console](https://aws.amazon.com/console/), search “CloudFormation’ in the search bar and navigate to the service dashboard. 
In the primary region (`us-east-1(N. Virginia)`) you should see two stacks: `CodeArtifactPrimaryStack-<region>` and `PackagePublishingPipelineStack`.

![image](https://user-images.githubusercontent.com/76660222/205584748-4d1f7a08-743c-4341-bb62-1a75b7ac9136.png)

Screenshot showing the CloudFormation Stacks in the primary region

Switch regions to one of the secondary regions `us-west-2 (Oregon)` or `us-east-2 (Ohio)` to see the remaining stacks named `CodeArtifactReplicaStack-<region>`. 
These correspond to the three AWS CDK Stacks from the architecture diagram.

![image](https://user-images.githubusercontent.com/76660222/205585032-1840b374-af2e-4753-954a-e3888af93a62.png)

Screenshot showing the CloudFormation stacks in a separate region


## Viewing the CodePipeline Package Publishing Pipeline

From the Console, select the primary region (`us-east-1`) and navigate to `CodePipeline` by utilizing the search bar.
Select the Pipeline titled `packagePipeline` and inspect the state of the pipeline.
This pipeline triggers after every commit from the CodeCommit repository named `PackageSourceCode`. 
If the pipeline is still in process, then wait a few minutes, as this pipeline can take approximately 7–8 minutes to complete all three stages (Source, Build, and Publish).
Once it’s complete, the pipeline should reflect the following screenshot:

![image](https://user-images.githubusercontent.com/76660222/205585510-a8f5ddda-e3d5-4607-bdbe-4812dcbbf936.png)
 A screenshot showing the CodePipeline flow
 
 ## Viewing the Published Package in the CodeArtifact Repository

To view the published artifacts, go to the primary or secondary region and navigate to the CodeArtifact dashboard by utilizing the search bar in the Console. You’ll see a repository named `package-artifact-repo`. Select the repository and you’ll see the sample pip package named `mypippackage` inside the repository. This package is defined by the source code in the CodeCommit repository named `PackageSourceCode` in the primary region (`us-east-1`).

![image](https://user-images.githubusercontent.com/76660222/205586049-262521f0-2404-4e0a-8c89-9bba4827bdbd.png)
Screenshot of the package repository

## Create a new package version in CodeCommit and monitor the pipeline release

Navigate to your CodeCommit’s PackageSourceCode (us-east-1 CodeCommit > Repositories > PackageSourceCode. Open the `setup.py` file and select the Edit button. Make a simple modification, change the `version = '1.0.0'` to `version = '1.1.0'` and commit the changes to the Main branch.

![image](https://user-images.githubusercontent.com/76660222/205586387-11faa6a8-aa57-4cf4-8880-db9931f41da9.png)
 A screenshot of the source package’s code repository in CodeCommit
 
 Now navigate back to CodePipeline and watch as the pipeline performs the release automatically. When the pipeline finishes, this new package version will live in each of the three CodeArtifact Repositories.
 
 ## Install the custom pip package to your local Python Environment

For your development team to connect to this CodeArtifact Repository to download repositories, you must configure the `pip` tool to look in this repository. From your Cloud9 IDE (or local development environment), let’s test the installation of this package for Python3:

1. Copy the connection instructions for the pip tool. Navigate to the CodeArtifact repository of your choice and select **View connection instructions**
   1. Select **Copy** to copy the snippet to your clipboard

![image](https://user-images.githubusercontent.com/76660222/205586563-cd61a163-2ade-4569-95a1-e1f7d1421a88.png)
Screenshot showing directions to connect to a code artifact repository

* Paste the command from your clipboard
* Run `pip install mypippackage==1.0.0`
![image](https://user-images.githubusercontent.com/76660222/205586717-33fcd402-ddaa-4f84-8378-7a493a46d5fc.png)

Screenshot showing CodeArtifact login

* Test the package works as expected by importing the modules
* Start the Python REPL by running `python3` in the terminal

![image](https://user-images.githubusercontent.com/76660222/205586837-b14d5d77-6d4c-43d8-99b7-be7e194e755c.png)

Screenshot of the package being imported


## Clean up

Destroy all of the AWS CDK Stacks by running `cdk destroy --all` from the root AWS CDK application directory.

![image](https://user-images.githubusercontent.com/76660222/205587321-e91d77f7-e8c1-4349-a584-5b9de6e37ba6.png)

![image](https://user-images.githubusercontent.com/76660222/205587604-dc6a33b5-72a5-4946-98bc-c6e2d4da9fa1.png)





