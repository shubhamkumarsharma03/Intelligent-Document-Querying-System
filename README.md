# AWS Bedrock Knowledge Base with Aurora Serverless

This project sets up an AWS Bedrock Knowledge Base integrated with an Aurora Serverless PostgreSQL database. It also includes scripts for database setup and file upload to S3.

## Table of Contents

1. [Project Overview](#project-overview)
2. [Prerequisites](#prerequisites)
3. [Project Structure](#project-structure)
4. [Deployment Steps](#deployment-steps)
5. [Using the Scripts](#using-the-scripts)
6. [Customization](#customization)
7. [Troubleshooting](#troubleshooting)

## Project Overview

This project consists of several components:

1. Stack 1 - Terraform configuration for creating:
   - A VPC
   - An Aurora Serverless PostgreSQL cluster
   - s3 Bucket to hold documents
   - Necessary IAM roles and policies

2. Stack 2 - Terraform configuration for creating:
   - A Bedrock Knowledge Base
   - Necessary IAM roles and policies

3. A set of SQL queries to prepare the Postgres database for vector storage
4. A Python script for uploading files to an s3 bucket

The goal is to create a Bedrock Knowledge Base that can leverage data stored in an Aurora Serverless database, with the ability to easily upload supporting documents to S3. This will allow us to ask the LLM for information from the documentation.

## Prerequisites
# AWS Bedrock Knowledge Base with Aurora Serverless

This repository contains an implementation that integrates an AWS Bedrock Knowledge Base with an Aurora Serverless PostgreSQL database and supporting scripts and Terraform stacks.

---

## Personal / Submission Details (replace before submitting)

 - **Name:** Shubham Kumar Sharma
 - **Email:** shubhamsharma86900@gmail.com
 - **GitHub repo (this project):** `https://github.com/shubhamkumarsharma03/Intelligent-Document-Querying-System`


---

## Quick Summary (for reviewer)
- Project: Bedrock Knowledge Base + Aurora Serverless integration
- Infrastructure: Managed with Terraform (two stacks: `stack1` and `stack2`)
- Scripts: Database preparation and S3 upload scripts in `scripts/`
- Screenshots & outputs: All output and necessary screenshots are in the `Screenshot/` folder
- Evaluation / model snippets: See 'bedrock_utils.py', 'temperature_top_p_explanation.pdf' or 'code_snippits.txt' (evaluation and prompt validation snippets)

---

## Table of Contents
1. [Project Overview](#project-overview)
2. [Prerequisites](#prerequisites)
3. [Project Structure](#project-structure)
4. [Model Parameters (included)](#model-parameters-included)
5. [Deployment Steps](#deployment-steps)
6. [Using the Scripts](#using-the-scripts)
7. [Evaluation / Code Snippets Locations](#evaluation--code-snippets-locations)
8. [Screenshots & Deliverables](#screenshots--deliverables)
9. [Submission Checklist](#submission-checklist)

---

## Project Overview

This project sets up an AWS Bedrock Knowledge Base integrated with an Aurora Serverless PostgreSQL database. It includes Terraform stacks to provision the infrastructure, SQL to prepare the database for vector storage, and Python utilities to upload files to S3 and interact with Bedrock and the Knowledge Base.

## Prerequisites

- AWS CLI installed and configured
- Terraform installed (compatible version used to create stacks in this repo)
- Python 3.10+ and `pip`
- AWS account with permissions for Bedrock, RDS/Aurora, S3, IAM and related resources

## Project Structure

```
project-root/
├── stack1/                # VPC, Aurora Serverless, S3, IAM
├── stack2/                # Bedrock Knowledge Base stack
├── modules/               # Terraform modules
├── scripts/               # Upload and DB setup scripts
│   ├── aurora_sql.sql
│   └── upload_to_s3.py
├── Screenshot/            # All screenshots and output images (for submission)
├── bedrock_utils.py       # Bedrock and KB helper functions (evaluation snippets)
├── code_snippits.txt      # Extracted snippets used during evaluation and testing
├── model_parameters.txt   # Explanation of temperature and top_p used for models
├── requirements.txt       # Python dependencies
└── README.md
```

## Model Parameters (included)

The contents of `model_parameters.txt` are included below for reviewer convenience:

```
Temperature (Controls Creativity and Randomness)

Temperature is a parameter that determines how “creative” or “risky” the model can be when generating responses.
A low temperature (e.g., 0.0–0.3) makes the model more deterministic, meaning it will consistently produce the same answer with minimal variation. This is ideal for technical answers, fact-based questions, or using knowledge base context.

A higher temperature (0.7–1.0) increases randomness and creativity, allowing the model to explore more diverse phrasing or ideas. This is useful for brainstorming or storytelling, but not recommended for accurate technical content.

Top-p (Controls Concentration of Probability Distribution)

Top-p, or nucleus sampling, controls how much of the probability distribution the model considers when generating each token.
A top-p = 1.0 means the model looks at all possible tokens, resulting in richer and more varied responses.
A lower top-p (like 0.1–0.3) restricts the model to only the most likely tokens, ensuring high precision and reducing the chance of irrelevant or incorrect answers.

In most Bedrock applications, temperature and top-p are used together to balance creativity and accuracy.
```

## Deployment Steps (short)

1. Clone this repository.
2. `cd stack1` -> `terraform init` -> `terraform apply` (follow prompts)
   - Stack 1 provisions VPC, Aurora Serverless Postgres, S3, and IAM resources.
3. Prepare the Aurora DB using `scripts/aurora_sql.sql` (use RDS Query Editor or psql against the DB endpoint).
4. `cd ../stack2` -> `terraform init` -> `terraform apply`
   - Stack 2 provisions the Bedrock Knowledge Base and associated roles.
5. Upload PDFs or documents placed in `spec-sheets/` to S3:
   ```pwsh
   python .\\scripts\\upload_to_s3.py
   ```
6. Sync or configure the knowledge base data source in Bedrock so documents are retrievable by the LLM.

## Using the Scripts

- `scripts/upload_to_s3.py` uploads the files from `spec-sheets/` to the configured S3 bucket. Update the bucket name in the script before running.
- `scripts/aurora_sql.sql` contains the SQL statements required to prepare the Postgres schema for vector/document storage.

## Evaluation / Code Snippets Locations

- The prompt validation and evaluation snippets used during testing are implemented in `bedrock_utils.py`.
  - Key functions: `valid_prompt`, `query_knowledge_base`, and `generate_response`.
- A plain-text copy of these and other snippet examples are included in `code_snippits.txt` for quick review.

Example: The `valid_prompt` function uses Bedrock model calls to categorize a user prompt before invoking the KB or model.

## Screenshots & Deliverables

- All screenshots and output captures used for evidence and evaluation are located in the `Screenshot/` folder at repository root.
- Please review that folder for the images you want to include with your Udacity submission.



