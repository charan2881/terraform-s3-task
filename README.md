\# Terraform S3 Bucket — Provisioning a Tagged, Versioned S3 Bucket



\## 📌 Overview



This project demonstrates the use of \*\*Terraform\*\* to provision and manage an AWS S3 bucket using Infrastructure as Code (IaC).



The bucket is configured with:



\* Environment-based naming using a Terraform variable

\* S3 bucket versioning

\* Resource tags

\* Terraform outputs for the bucket name and ARN

\* AWS provider configuration



This assessment was completed as an introductory Terraform exercise to understand how Terraform provisions AWS resources, manages dependencies, and exposes resource information through outputs.



\---



\## 🎯 Objective



The objective of this assessment was to:



1\. Create an AWS S3 bucket using Terraform.

2\. Use a variable for the environment.

3\. Enable S3 versioning using a separate `aws\_s3\_bucket\_versioning` resource.

4\. Add appropriate tags to the bucket.

5\. Output the S3 bucket name and ARN.

6\. Verify the Terraform configuration using `terraform plan` and `terraform apply`.

7\. Clean up the resources using `terraform destroy`.



\---



\## 🛠️ Technologies Used



\* \*\*Terraform:\*\* v1.16.3

\* \*\*Cloud Provider:\*\* AWS

\* \*\*AWS Service:\*\* Amazon S3

\* \*\*Operating System:\*\* Windows

\* \*\*Terminal:\*\* Git Bash

\* \*\*Version Control:\*\* Git \& GitHub



\---



\## 📁 Project Structure



```text

terraform-s3-task/

│

├── main.tf

├── variables.tf

├── outputs.tf

└── README.md

```



\### `main.tf`



Contains:



\* Terraform AWS provider configuration

\* S3 bucket resource

\* S3 bucket versioning resource

\* Bucket tags



\### `variables.tf`



Contains the `environment` variable with a default value of `dev`.



\### `outputs.tf`



Contains outputs for:



\* S3 bucket ARN

\* S3 bucket name



\---



\## ⚙️ Configuration



\### Environment Variable



The project uses the following Terraform variable:



```hcl

variable "environment" {

&#x20; type    = string

&#x20; default = "dev"

}

```



This variable is used when constructing the S3 bucket name.



Example:



```text

anyops-logs-dev-<initials>

```



\---



\## 🪣 S3 Bucket Configuration



The S3 bucket is created using:



```hcl

resource "aws\_s3\_bucket" "logs" {

&#x20; bucket = "anyops-logs-${var.environment}-<initials>"



&#x20; tags = {

&#x20;   Environment = var.environment

&#x20;   Owner       = "<your name>"

&#x20; }

}

```



The bucket name uses the environment variable dynamically.



\---



\## 🔄 S3 Versioning



Versioning is enabled using a \*\*separate Terraform resource\*\*, as required by the assessment:



```hcl

resource "aws\_s3\_bucket\_versioning" "logs" {

&#x20; bucket = aws\_s3\_bucket.logs.id



&#x20; versioning\_configuration {

&#x20;   status = "Enabled"

&#x20; }

}

```



This demonstrates how Terraform resources can be linked together.



The versioning resource references the S3 bucket using:



```hcl

aws\_s3\_bucket.logs.id

```



\---



\## 🏷️ Tags



The S3 bucket is tagged with:



```text

Environment = dev

Owner       = <your name>

```



Tags help identify and organize AWS resources.



\---



\## 📤 Terraform Outputs



The project outputs the S3 bucket's ARN and name.



Example:



```hcl

output "bucket\_arn" {

&#x20; description = "ARN of the S3 bucket"

&#x20; value       = aws\_s3\_bucket.logs.arn

}



output "bucket\_name" {

&#x20; description = "Name of the S3 bucket"

&#x20; value       = aws\_s3\_bucket.logs.id

}

```



\---



\# 🚀 Steps Performed



\## 1. Created the Terraform Project



Created a project directory:



```text

terraform-s3-task

```



Created the following Terraform files:



```text

main.tf

variables.tf

outputs.tf

```



\---



\## 2. Configured the AWS Provider



Configured Terraform to use the AWS provider and the `ap-south-1` region.



\---



\## 3. Declared the Environment Variable



Created an `environment` variable with:



```text

type = string

default = "dev"

```



\---



\## 4. Created the S3 Bucket



Provisioned an S3 bucket using the required naming convention:



```text

anyops-logs-${var.environment}-<initials>

```



\---



\## 5. Added Resource Tags



Added:



```text

Environment = dev

Owner = <your name>

```



\---



\## 6. Enabled S3 Versioning



Configured S3 versioning through the separate:



```text

aws\_s3\_bucket\_versioning

```



resource.



\---



\## 7. Initialized Terraform



Executed:



```bash

terraform init

```



Terraform successfully initialized the project and configured the required AWS provider.



\---



\## 8. Validated the Configuration



Executed:



```bash

terraform plan

```



The configuration was checked by Terraform to determine the required infrastructure changes.



\---



\## 9. Applied the Configuration



Executed:



```bash

terraform apply

```



and confirmed the deployment when prompted.



\---



\## 10. Verified the AWS Resource



Verified the S3 bucket through the AWS Console.



Checked:



\* Bucket creation

\* Bucket name

\* Versioning status

\* Resource tags



\---



\## 11. Verified Terraform Outputs



Executed:



```bash

terraform output

```



to verify the S3 bucket name and ARN.



\---



\## 12. Destroyed the Resources



After completing the assessment, the infrastructure can be removed using:



```bash

terraform destroy

```



This prevents unnecessary AWS resources from remaining active.



\---



\# 📚 Key Concepts Learned



Through this exercise, I learned the fundamentals of Terraform and Infrastructure as Code, including:



\* Terraform providers

\* Terraform resources

\* Terraform variables

\* Resource dependencies

\* AWS S3 provisioning

\* S3 versioning

\* Resource tagging

\* Terraform outputs

\* `terraform init`

\* `terraform plan`

\* `terraform apply`

\* `terraform destroy`

\* Basic Terraform project structure



\---



\## ✅ Assessment Outcome



Successfully created a Terraform configuration for provisioning a \*\*tagged and versioned AWS S3 bucket\*\*, including environment-based naming and Terraform outputs for the bucket ARN and name.



This project serves as a basic introduction to managing AWS infrastructure using Terraform and Infrastructure as Code.



