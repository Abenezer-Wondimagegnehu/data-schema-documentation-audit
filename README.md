# Data Schema Documentation Audit

This repository contains an audit of the Berlin source data schema, comparing the production database structure against its existing documentation. The analysis identifies gaps in table coverage, column mappings, data types, constraints, and provides recommendations for improvements. It was conducted using Jupyter notebooks for schema inspection and Excel for detailed gap tracking.

Key outcomes include:
- Identification of undocumented tables and columns.
- Metrics on mismatches (e.g., data types, constraints).
- Proposed definitions for undocumented fields and schema enhancements.

This project demonstrates skills in data auditing, schema validation, Python (with libraries like pandas and openpyxl), and documentation best practices.

## Description
Audits database schema documentation by comparing schema metadata with documented definitions. Identifies missing or inconsistent table and column descriptions and produces structured recommendations. Uses sample metadata in place of live database access for public demonstration.

## Problem Statement
Poor or outdated schema documentation leads to confusion, onboarding delays, and data misuse. This project demonstrates how to systematically audit schema documentation quality and identify gaps.

## Approach
- Simulate database schema metadata
- Compare documented vs actual table and column definitions
- Detect missing or inconsistent documentation
- Generate structured audit findings and recommendations

## Configuration Options
This project is designed for public demonstration and does not require live database credentials.

If extended to a real environment:
- Database credentials should be stored in a `.env` file
- Environment variables should be loaded securely
- `.env` files must not be committed to version control

## Security Notice
No real database credentials are included. Sample metadata is used to safely demonstrate production-grade documentation audit workflows.

## Tech Stack
- Python
- SQLAlchemy
- PostgreSQL (simulated)
- Spreadsheets

## Repository Structure

The repository is organized as follows for clarity and maintainability:

data-schema-documentation-audit/
├── docs/                         # Documentation and summary reports
│   └── audit_summary.md          # Detailed Markdown summary of the database vs. documentation gap analysis
├── notebooks/                    # Jupyter notebooks for analysis and code execution
│   └── schema_audit.ipynb        # Main notebook for schema review, inspections, and validations
├── outputs/                      # Generated artifacts and results
│   └── documentation_gaps.xlsx   # Excel spreadsheet with column-by-column comparisons and metrics
├── .gitignore                    # Git ignore file to exclude temporary or sensitive files
├── LICENSE                       # License file (e.g., MIT) for the project
└── README.md                     # This file: Project overview and repository guide


- **docs/**: Holds human-readable summaries and reports, such as the full gap analysis.
- **notebooks/**: Contains interactive code for the audit process (e.g., querying schemas, comparing data).
- **outputs/**: Stores non-code outputs like spreadsheets; these can be regenerated from notebooks if needed.
- Root files: Essential for project setup and licensing.

