---
description: Scans and create Pact contracts for the specified folders
argument-hint: [folder1] [folder2] ... (if none specified, only the current folder will be scanned)
---

# Pact Scan
This command scans and create Pact contracts for the specified folders.

## Context
Role: Researcher
Read the following documentation to understand how to create Pact contracts:
https://docs.pact.io/consumer
https://docs.pact.io/getting_started/conceptual_overview
https://docs.pact.io/getting_started/how_pact_works
https://docs.pact.io/getting_started/matching 
https://docs.pact.io/getting_started/terminology
https://docs.pact.io/getting_started/verifying_pacts
https://docs.pact.io/recipes/apigateway
https://docs.pact.io/recipes/kafka
https://github.com/pact-foundation/pact-specification/tree/version-3
If you need more sources feel free to register them
Contract verification is not part of this project.
The goal is to create contracts for the current project.

### Some additional notes:
- Pact Broker: https://pact.bynder.cloud/. Consumer participant asset-svc; provider names suggested as pybynder, platform-storage, cae/converter, boss-integration, portal (confirm exact spellings when registering).
- Library: pact4s (io.github.jbwheatley) — pact4s-scalatest (HTTP) + pact4s-messages (Kafka), matching Scala 3.3.4 + ScalaTest.
- Pact protobuf plugin: not available → BossIntegrationConsumer (2 contracts) is blocked until provisioned.
- FileMetadataExtracted: flagged as not suitable for contract testing (dynamic per-file XMP payload, no stable schema) → excluded, revisit only if a guaranteed-minimum field subset is standardised. 
- Whitelisted Portal ids (hardcoded in model/portals/package.scala:4-5): FEATURE_PACKAGE_ANALYSIS = "e2d814c2-6c83-412d-9c4b-70a8ec71644d", SETTING_PACKAGE_RELATION_METAPROPERTY = "22c84e9f-afb0-4704-9012-940657116152". 
- Resolved decisions (cont.)
- pybynder error responses: the provider does not guarantee a response body on non-200/404 statuses (e.g. 5xx may have no body). The getLinkedMetaproperty contract therefore pins only the 200 and 404 status codes — no body, no other-status interaction.

## Process
If $ARGUMENTS is empty, then scan only the current folder else scan the specified folders.
for each folder start search for the following HTTP clients or Kafka consumers:

### HTTP clients
For each HTTP client register the following information
- base url
- method
- path
- response type
- Register what we do with the response body. If its JSON then register which properties we use from the result object.

Feature flag managers like Split.io are excluded since they non-contractable. 

### gRPC clients
gRPC clients are excluded, as they are already contract-based.

### Kafka consumers
For each Kafka consumer register the following information
- Consumer group name
- topic
- value
The value contains a header and a body. From both parts we would like to know which properties use to create the contract.

## Output
As output want to create a report with the following information following this format:
Foreach an http client, create a table with the following columns:
- Folder
- method
- base url
- path
- response type
- properties used to create the contract

Each HTTP client will consist of three parts
- table row that match each column with the corresponding value
- Under the table the contract printed in JSON format.
- Under the contract, next times for implementation of the contract is described.
  The third needs to be agent friendly, it should describe what needs to be done in this 
  repo so that a planning agent can pick this up and create tasks for it. Follow the pattern below
  ```
  Title: [Provide task name for the implementation start with AGENT-WORK: ]
  Context: [provide all context needed to implement the contract]
  Description: [provide a extendsive description of what needs to be done]
  Reasoning: [provide a reasoning why this is needed]
  ```
  if input of the user is needed then please ask. 

For each Kafka consumer, create a table with the following columns:
- Folder
- Consumer group name
- topic
- properties used to create the contract

Each Kafka consumer will get three rows
- table row that match each column with the corresponding value
- Under the table the contract printed in JSON format.
- Under the contract, next times for implementation of the contract is described.
  The third needs to be agent friendly, it should describe what needs to be done in this
  repo so that a planning agent can pick this up and create tasks for it. Follow the pattern below
  ```
  Title: [Provide task name for the implementation start with AGENT-WORK: ]
  Context: [provide all context needed to implement the contract]
  Description: [provide a extendsive description of what needs to be done]
  Reasoning: [provide a reasoning why this is needed]
  ```
  if input of the user is needed then please ask.

The next part of the report adds a table with the following columns:
- Folder
- Total number of contracts

The last part of the report contains resources that you needed but were not specified.
So that I can provide better context next time. 

Write the report to a file called PACT_CONTRACTS.md in the project root directory.
