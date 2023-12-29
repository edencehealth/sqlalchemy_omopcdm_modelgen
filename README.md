# `sqlalchemy_omopcdm_modelgen`

This repo contains the source code for the tool we use to generate the model files in our [`edencehealth/sqlalchemy_omopcdm` repo](https://github.com/edencehealth/sqlalchemy_omopcdm).

The source code in this repo is a containerized Python program which:

- downloads the official OHDSI OMOP CDM DDL files
- applies the DDL files to a PostgreSQL database server
- applies [edenceHealth custom DDL](src/modelgen/sql/eh_mods.sql) which adds composite primary keys to the tables that don't have a natural primary key
- uses the tool [`sqlacodegen`](https://pypi.org/project/sqlacodegen/) to scan that database to generate a [Declarative Mapping](https://docs.sqlalchemy.org/en/20/orm/mapping_styles.html#orm-declarative-mapping)-based SQLAlchemy 2 model for each table in the OMOP CDM, including primary keys, indexes, and constraints
- rewrites the generated model using [`libcst`](https://pypi.org/project/libcst/) to:
    - add doc comments (from the [official OMOP CDM documentation website](https://ohdsi.github.io/CommonDataModel/cdm54.html)),
    - insert relevant pylint "disable" comments
    - renames the generated base class
- formats the resulting python module with the PSF tools [`black`](https://pypi.org/project/black/) and [`isort`](https://pypi.org/project/isort/)
