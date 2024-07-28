# AIGoat : A Deliberately Vulnerable AI Infrastructure


<div align="center">
  <img src="frontend/public/images/aigoat_banner.jpg" alt="aigoat_banner" width="500"/>
</div>

## Table of Contents

* [Description](#Description)
  * [Tech Stack](#Tech-Stack)
  * [Vulnerabilities](#Vulnerabilities)
* [Getting Started](#Getting-Started)
  * [Prerequisites](#Prerequisites)
  * [Usage](#Usage)
  * [Manual Installation](#Manual-Installation)
* [Attack Scenarios](#Attack-Scenarios)
* [Pricing](#Pricing)
* [Contributors](#Contributors)
* [Solutions](#Solutions)
* [Presented at](#Presented-at)
* [Contribution Guidelines](#Contribution-Guidelines)
* [License](#License)

# Description

Insecure AI infrastructure can expose organizations to significant risks, including data breaches and manipulation of AI-driven decisions. Often, these vulnerabilities arise from misconfigurations or overlooked security flaws in AI models, applications and deployment environments. Given the complexity of AI systems, many developers and data scientists are unaware of these potential threats, leading to vulnerable AI deployments.

AI-Goat is a deliberately vulnerable AI infrastructure hosted on AWS, designed to simulate the [OWASP Machine Learning Security Top 10 risks](https://owasp.org/www-project-machine-learning-security-top-10/) (OWASP ML Top 10). AI-Goat replicates real-world AI cloud deployment environments but introduces vulnerabilities intentionally to provide a realistic learning platform. It features multiple attack vectors and is focused on a black-box testing approach.

AI-Goat uses Infrastructure as Code (IaC) with Terraform to deploy the vulnerable infrastructure on the user's AWS account. This approach gives users full control over the code, infrastructure, and environment. By using AI-Goat, users can learn and practice:

AI Security Testing/Red-teaming<br />
AI Infrastructure as Code<br />
Understanding vulnerabilities in AI application infrastructure<br />
Identifying risks in the services and tools that interact with AI applications

The project is structured into modules, representing a distinct AI application with different tech stacks. AI-Goat leverages IaC through Terraform and GitHub Actions to simplify the deployment process.


## Tech Stack

* AWS
* React
* Python 3
* Terraform

## Vulnerabilities

The project aims to cover all major vulnerabilities in the OWASP Machine Learning Security Top 10.
Currently, the project includes the following vulnerabilities/risks:

* ML02:2023 Data Poisoning Attack
* ML06:2023 AI Supply Chain Attacks
* ML09:2023 Output Integrity Attack

# Getting Started

### Prerequisites
* An AWS Account + AWS Access Key with Administrative Privileges

### Usage

To simplify the deployment process, users can fork this repository, add their AWS account credentials to GitHub secrets, and run the Terraform Apply Action. This workflow will deploy the entire infrastructure and provide the URL of the hosted application.

Here are the steps to follow:

**1.** Fork the repo

**2.** Set the GitHub Action Secrets inside settings/secrets with the following keys:

```
AWS_ACCESS_KEY
AWS_SECRET_ACCESS_KEY
```

<p align="center">
  <img src="frontend/public/images/github_actions.jpg">
</p>

**Step 3.** From the repository actions tab run the ``Terraform Apply`` Workflow.

**Step 4.** Find the application URL in the Terraform output section.

<p align="center">
  <img src="TBD">
</p>


### Manual Installation

If you wish to manually deploy AIGoat, follow these steps:

**Step 1.** Clone the repo
```sh
git clone https://github.com/orcasecurity-research/AIGoat
```

**Step 2.** Configure AWS User Account Credentials
```sh
aws configure
```

**Step 3.** Traverse into the respective modules' directory and use terraform to deploy AWSGoat
```sh
cd terraform
terraform init
terraform apply --auto-approve
```

# Attack Scenarios

All scenarios within AI-Goat are part of a toy store application featuring different machine learning functionalities. Each scenario is designed to demonstrate specific vulnerabilities from the OWASP Machine Learning Security Top 10 risks.

**Scenario 1:** AI Supply Chain Attacks
This scenario features a product search page within the application. Users can upload an image, and the ML model calculates and displays the most similar products. 
This module highlights vulnerabilities in the AI supply chain, where attackers can compromise the pipeline due to a vulnerable package.<br />
**Goal:** Compromise the product search functionality using the file upload option to achieve Server-Side Request Forgery (SSRF) on the hosted machine and gain remote code execution.

Architecture:

<p align="center">
  <img src="architecture image">
</p>


**Scenario 2:** Data Poisoning Attack
This scenario involves a custom product recommendations model. When a user is logged in, the cart page displays personalized product recommendations. 
The scenario showcases vulnerabilities in the AI model training process and dataset, allowing attackers to poison the data and manipulate recommendations.<br />
###### Login with these credentials to view the recommendations: 
```
user: babyshark
password: doodoo123
```
**Goal:** Manipulate the AI model to recommend a product - Orca Doll, which is not visible in the catalog for the provided user.

Architecture:

<p align="center">
  <img src="architecture image">
</p>

 Note: The Orca Doll product is not visible in the catalog.

**Scenario 3:** Output Integrity Attack
For this scenario, the application features a content and spam filtering AI system that checks each comment a user attempts to add to a product page. The AI determines whether the comment is allowed or not. This module demonstrates vulnerabilities in the model output integrity, where attackers can manipulate the AI system to bypass content filtering.<br />

**Goal:** Bypass the content filtering AI system to post on the Orca Doll product page the forbidden comment: 
``` 
"pwned"
``` 
Success is achieved this comment that should be filtered gets published.

Architecture:

<p align="center">
  <img src="architecture image">
</p>


# Pricing

The resources created with the deployment of AIGoat will have the following charges for the US-East region: 

Total: **$0.0125/hour** - TBD

# Contributors

Ofir Yakobi, Security Researcher, Orca Security  <ofir.yakobi@orca.security>

Shir Sadon, Security Researcher, Orca Security <shir.sadon@orca.security>

# Solutions

Spoiler alert! Avoid browsing the repository files as they contain spoilers :smiley:.

The solutions are available in the [solutions](solutions/) directory.

## Presented at

- [Appsec Village DC 32: Arsenal](https://www.appsecvillage.com/events/dc-2024/arsenal-ai-goat-707694)

## Contribution Guidelines

* Contributions in the form of code improvements, module updates, feature improvements, and any general suggestions are welcome. 
* Improvements to the functionalities of the current modules are also welcome. 
* The source code for each module can be found in ``terraform/modules/<module_name>/main.tf`` this can be used to modify the existing application code.

# License

This program is free software: you can redistribute it and/or modify it under the terms of the MIT License.

You should have received a copy of the MIT License along with this program. If not, see https://opensource.org/licenses/MIT.