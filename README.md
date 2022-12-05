# vigilant-adventure
Created a Multi-Region Python Package Publishing Pipeline with AWS CDK and CodePipeline

This repository addresses how a custom solution built with the AWS Cloud Development Kit and AWS CodePipeline can create a Multi-Region Python Package Publishing Pipeline.

Whether it’s for resiliency or performance improvement, many customers want to deploy their applications across multiple regions. When applications are dependent on custom software packages, the software packages should be replicated to multiple regions as well. This repository will walk through how to deploy a custom package publishing pipeline in your own AWS Account. This pipeline connects a Python package source code repository to build and publish pip packages to CodeArtifact Repositories spanning three regions (the primary and two replica regions). While this sample CDK Application is built specifically for pip packages, the underlying architecture can be reused for different software package formats, such as npm, Maven, NuGet, etc.

Solution overview
The following figure demonstrates the solution workflow:

A CodePipeline pipeline orchestrates the building and publishing of the software package
This pipeline is triggered by commits on the main branch of the CodeCommit repository
A CodeBuild job builds the pip packages using twine to be distributed
The publish stage (third column) uses three parallel CodeBuild jobs to publish the distribution package to the two CodeArtifact repositories in separate regions
The first CodeArtifact Repository stores the package contents in the primary region.
The second and third CodeArtifact Repository act as replicas and store the package contents in other regions.
![image](https://user-images.githubusercontent.com/76660222/205563417-95efdb87-bef9-412b-b161-8c951d2a5b91.png)

Figure 1.  Architecture diagram

All of these resources are defined in a single AWS CDK Application. The resources are defined in CDK Stacks that are deployed as AWS CloudFormation Stacks. AWS CDK can deploy the different stacks across separate regions.
