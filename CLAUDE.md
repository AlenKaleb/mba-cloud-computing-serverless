# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Code collection for the FullCycle MBA Cloud Computing Serverless course. Each artifact corresponds to a practical lesson ("aula") and is meant to be deployed to AWS (Lambda, ECS/ECR, S3) rather than run as a cohesive local application. Per the README, the code is intentionally simple demo material — no extensive patterns, rules, or tests are expected. Comments and strings are in Portuguese.

**Before deploying anything, scan the code for comments asking for substitutions** (account-specific values such as queue URLs, table names, parameter/secret names, regions). The README explicitly calls this out as required for the code to work.

## Repository Layout

- `lambdas/` — AWS Lambda functions, one per lesson:
  - `function-aula-9/`, `function-aula-10/`, `function-aula-11/` — Java/Quarkus (3.10.0) Lambda functions committed as **exploded build artifacts** (compiled `.class` files plus `lib/*.jar` dependencies and `application.properties`), not source code. There is no Java source or build file for these in the repo; treat them as deployment snapshots from the lessons.
  - `function-aula-15.py` … `function-aula-20.py` — single-file Python handlers (`lambda_handler(event, context)`) using `boto3`, each demonstrating one integration: 15 = API Gateway proxy routing, 16 = DynamoDB, 17 = SQS, 18 = EC2, 19 = SSM Parameter Store, 20 = Secrets Manager. Region is hardcoded where used (`us-east-1`).
- `ecs/aulas-12-13/` — Spring Boot 3.2.5 / Java 17 Maven app (`java-ecs-spring`) used for the ECR/ECS lessons. Exposes a single REST endpoint `GET /teste-aws?nome=...` (`TesteAws.java`). Includes a `Dockerfile` that packages the built jar.
- `files/` — JSON files used for S3 upload exercises.

## Commands

Only the ECS app has a local build. From `ecs/aulas-12-13/`:

```bash
./mvnw spring-boot:run        # run locally on :8080
./mvnw test                   # runs the single Spring context test
./mvnw clean package          # builds target/java-ecs-spring-0.0.1-SNAPSHOT.jar
docker build -t java-ecs .    # Dockerfile expects the jar from `package` above
```

The Python lambdas have no build, dependency manifest, or test harness — they are edited as standalone files and deployed directly to the AWS Lambda Python runtime. The Java lambda directories are build output and cannot be rebuilt from this repo.
