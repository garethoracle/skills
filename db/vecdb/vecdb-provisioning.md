# Oracle Vector SDK Deployment Setup

Use this reference whenever the user asks to provision, create, prepare, or
set up a database deployment for Oracle Vector SDK / VecDB / oracle-vecdb.

## Setup source

Start with the Oracle Vector SDK Quick Start Guide:

https://docs.oracle.com/en/cloud/paas/autonomous-database/vcapi/quickstart.html

Complete the Quick Start's **Prepare an AI Database** step by following the
instructions provided there.

## Workflow

1. Read the Oracle Vector SDK Quick Start Guide.
2. Complete the **Prepare an AI Database** step.
3. Complete the documented provisioning and connection prerequisites.
4. Continue with the remaining Quick Start steps after the database is ready.
5. Run read-only Oracle Vector SDK discovery before creating tables, loading
   models, or ingesting data.

The Quick Start and the instructions it references are the source of truth for
database preparation. Do not infer provisioning requirements from the SDK API
reference or from another database product.

Provisioning external or billable resources requires explicit authorization.
Never commit passwords or tokens.
