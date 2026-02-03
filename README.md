# data-schema-documentation-audit

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
