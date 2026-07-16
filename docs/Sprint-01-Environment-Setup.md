# Sprint 01 – Environment Setup

> Project: Enterprise Data Engineering Lab
>
> Sprint Goal:
> Build a production-ready local environment for Data Engineering using SQL Server, VS Code, Python, Git, Docker, and AdventureWorks.

---

# Sprint Overview

The first sprint focused on preparing a professional Data Engineering environment instead of immediately writing code.

In enterprise projects, setting up the development environment correctly is critical because every subsequent stage—including data ingestion, ETL, Spark, orchestration, and analytics—depends on it.

The objective of this sprint was to create a stable SQL Server environment and restore a realistic enterprise database that will be used throughout the entire project.

---

# Learning Objectives

By the end of this sprint I should be able to:

- Understand the software required for Data Engineering.
- Install SQL Server correctly.
- Configure SQL Server for future Python and Spark connectivity.
- Restore an enterprise database.
- Explore the structure of a production database.
- Understand the business behind the database before writing SQL.

---

# Software Stack

| Software | Purpose |
|----------|---------|
| VS Code | Main IDE |
| Git | Version Control |
| GitHub | Repository Hosting |
| Python | Data Engineering Programming |
| Docker Desktop | Containerization (planned for later services) |
| SQL Server 2025 Developer | Enterprise Relational Database |
| SSMS | SQL Server Administration |
| AdventureWorks2025 | Enterprise Sample Database |

---

# Why These Tools?

## VS Code

Chosen because it supports:

- Python
- SQL
- PySpark
- Git
- Docker
- Azure
- Databricks

One IDE is sufficient for the complete project.

---

## Git

Every Data Engineer should version control pipelines and SQL scripts.

Git allows:

- collaboration
- rollback
- branching
- code review

---

## Python

Python is the primary programming language used for:

- ETL
- Data Ingestion
- Automation
- Spark
- Airflow

---

## SQL Server

Chosen because AdventureWorks is Microsoft's enterprise database.

It provides:

- realistic business schema
- multiple business domains
- relationships
- normalized database

---

## AdventureWorks

AdventureWorks represents a bicycle manufacturing company.

Instead of learning SQL on toy datasets, we learn using a realistic enterprise database.

---

# Installation Process

## Step 1

Installed

- VS Code
- Git
- Python
- Docker Desktop
- SQL Server Extension
- SQL Server 2025 Developer
- SSMS

---

## Step 2

Initially attempted SQL Server inside Docker.

Reason:

Containerized environments are common in enterprise development.

---

# Docker Issues

Attempted image:

```
mcr.microsoft.com/mssql/server:2022-latest
```

Error:

```
Get https://mcr.microsoft.com/v2/ : EOF
```

---

# Investigation

Verified:

✅ Docker Hub working

```
docker pull hello-world
```

Succeeded.

---

Verified MCR

```
curl https://mcr.microsoft.com/v2/
```

Returned

HTTP 200 OK

Meaning

Windows networking was correct.

---

Verified Docker Container

```
docker run --rm curlimages/curl -I https://mcr.microsoft.com/v2/
```

Returned

HTTP 200

Meaning Docker networking was also working.

---

Conclusion

The issue was specific to Docker daemon pulling SQL Server images from Microsoft Container Registry.

Instead of wasting additional development time, the decision was made to install SQL Server directly on Windows.

This reflects an important engineering principle:

> Remove blockers quickly and continue delivering value.

---

# SQL Server Installation Decisions

## Database Engine Services

Selected

Reason

This is the core SQL Server engine.

Without it SQL Server cannot host databases.

---

## SQL Server Replication

Not selected.

Reason

Replication is required only for high availability and distributed databases.

Not required for learning Data Engineering.

---

## AI Services

Not selected.

Reason

Used for machine learning inside SQL Server.

Our ML workloads will be performed using Python.

---

## Full Text Search

Not selected.

Reason

Used for advanced text searching.

Not required.

---

## PolyBase

Not selected.

Reason

PolyBase connects SQL Server with external systems.

Interesting technology but unnecessary during initial learning.

---

## Analysis Services

Not selected.

Reason

Analysis Services is used for OLAP cubes.

Modern Data Engineering uses Spark and Lakehouses instead.

---

## Integration Services (SSIS)

Not selected.

Reason

SSIS is Microsoft's ETL tool.

This project focuses on portable ETL pipelines built using:

- Python
- Spark
- Airflow

instead of vendor-specific tools.

---

# Instance Configuration

Selected

Default Instance

```
MSSQLSERVER
```

Reason

Default instance is easier to connect using:

```
localhost
```

instead of named instances.

---

# Server Configuration

Database Engine

Automatic

Reason

SQL Server starts automatically whenever Windows starts.

---

SQL Server Agent

Manual

Reason

SQL Agent is mainly used for scheduled SQL jobs.

Not required during development.

---

SQL Browser

Disabled

Reason

Browser service is mainly required for named instances.

We installed the default instance.

---

Perform Volume Maintenance Tasks

Enabled

Reason

Enables Instant File Initialization.

Benefits

- Faster restore
- Faster database creation
- Better performance

---

# Authentication Mode

Selected

Mixed Mode

Reason

Allows

- Windows Authentication
- SQL Authentication

Future tools like

- Python
- SQLAlchemy
- Spark
- Airflow

can use SQL Authentication.

---

# Why Add Current User?

Current Windows account was added as SQL Server Administrator.

Reason

Provides full administrative access.

Without it,

database management becomes difficult.

---

# Azure Extension

Initially prompted during installation.

Decision

Disabled.

Reason

Azure Extension is used only for Azure Arc integration.

This project runs completely on the local machine.

---

# Database Restore

Database

AdventureWorks2025.bak

Successfully restored.

---

# Why AdventureWorks?

AdventureWorks represents a real enterprise.

Business domains include

- Human Resources
- Production
- Purchasing
- Sales
- Customer Management

This allows learning Data Engineering on realistic business data.

---

# Database Exploration

Instead of immediately writing SQL,

the first task was understanding the business.

Business Flow

Supplier

↓

Purchasing

↓

Production

↓

Inventory

↓

Sales

↓

Customer

Understanding business processes before writing SQL is an important Data Engineering practice.

---

# Major Business Schemas

## HumanResources

Employees

Departments

Shift Management

---

## Person

Customer

Address

Contact

Email

Phone

---

## Production

Products

Categories

Manufacturing

Inventory

---

## Purchasing

Vendors

Purchase Orders

Procurement

---

## Sales

Customers

Orders

Invoices

Revenue

---

# Engineering Lessons Learned

## Lesson 1

Environment setup is part of engineering.

Writing code is only one stage of a project.

---

## Lesson 2

Understand the business before understanding tables.

Tables represent business processes.

---

## Lesson 3

Not every SQL Server feature needs to be installed.

Choose only what solves the current problem.

---

## Lesson 4

Avoid wasting time on infrastructure issues.

If an approach blocks progress,

choose another professional solution.

---

## Lesson 5

Enterprise databases are organized by business domains rather than random tables.

---

# Problems Faced

| Problem | Solution |
|----------|----------|
| Docker SQL Server image EOF | Installed SQL Server locally |
| Azure signup requested payment | Disabled Azure Extension |
| SQL Server connection confusion | Used localhost with Windows Authentication |
| Large number of tables | First understood business domains instead of tables |

---

# Sprint Achievement

✅ Installed complete Data Engineering environment.

✅ Installed SQL Server.

✅ Connected using SSMS.

✅ Restored AdventureWorks2025.

✅ Explored enterprise schemas.

✅ Understood the business represented by the database.

---

# Skills Acquired

- Environment Setup
- SQL Server Installation
- SQL Server Configuration
- Enterprise Database Restoration
- Database Exploration
- Business Understanding
- Engineering Decision Making
- Troubleshooting
- Documentation

---

# Interview Questions

### Why did you choose SQL Server?

### Why not install SSIS?

### Difference between Windows Authentication and Mixed Mode?

### Why use the default instance?

### Why restore AdventureWorks instead of using CSV files?

### Why understand business before writing SQL?

### Why wasn't Docker used eventually?

### What are the major schemas in AdventureWorks?

---

# Next Sprint

Sprint 02

Database Exploration & SQL Fundamentals

Goals

- Identify the most important tables.
- Understand relationships.
- Learn SQL querying.
- Build an Entity Relationship Diagram.
- Prepare for Python-based data ingestion.
