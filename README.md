# sqlalchemy_omopcdm_modelgen

This repo contains the source code for the tool we use to generate the model files in the [￼`edencehealth/sqlalchemy_omopcdm`￼ repo](https://github.com/edencehealth/sqlalchemy_omopcdm)

The source code in this repo is a containerized Python program which:

- downloads the official OHDSI OMOP CDM DDL files
- applies the DDL files to a PostgreSQL database server
- uses the tool [￼`sqlacodegen`￼](https://pypi.org/project/sqlacodegen/) to can the database then generate a `DeclarativeMapping`-based SQLAlchemy 2 model for each table in the OMOP CDM, including primary keys, indexes, and constraints
- rewrites the generated model using [￼`libcst`￼](https://pypi.org/project/libcst/) with doc comments from the official OMOP CDM documentation website, applies relevant pylint "disable" comments, renames the generated class, etc.
- formats the model with the PSF tools [￼`black`￼](https://pypi.org/project/black/) and [￼`isort`￼](https://pypi.org/project/isort/)
