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
https://github.com/pact-foundation/pact-specification/tree/version-4
If you need more sources feel free to register them
Contract verification is not part of this project.
The goal is to create contracts for the current project.

if local references cannot be found, use the global reference.

### Some additional notes:
- Pact Broker: https://pact.bynder.cloud/. Consumer participant asset-svc; provider names suggested as pybynder, platform-storage, cae/converter, boss-integration, portal (confirm exact spellings when registering).
- Library: pact4s (io.github.jbwheatley) — pact4s-scalatest (HTTP) + pact4s-messages (Kafka), matching Scala 3.3.4 + ScalaTest.
- Pact protobuf plugin: not available → BossIntegrationConsumer (2 contracts) is blocked until provisioned.
- FileMetadataExtracted: flagged as not suitable for contract testing (dynamic per-file XMP payload, no stable schema) → excluded, revisit only if a guaranteed-minimum field subset is standardised. 
- Whitelisted Portal ids (hardcoded in model/portals/package.scala:4-5): FEATURE_PACKAGE_ANALYSIS = "e2d814c2-6c83-412d-9c4b-70a8ec71644d", SETTING_PACKAGE_RELATION_METAPROPERTY = "22c84e9f-afb0-4704-9012-940657116152". 
- Resolved decisions (cont.)
- pybynder error responses: the provider does not guarantee a response body on non-200/404 statuses (e.g. 5xx may have no body). The getLinkedMetaproperty contract therefore pins only the 200 and 404 status codes — no body, no other-status interaction.

### List of repos from providers to register contracts for:
- git@github.com:Bynder/cae-audio-converter-svc.git
- git@github.com:Bynder/cae-dbupdater-svc.git
- git@github.com:Bynder/cae-derivative-svc.git
- git@github.com:Bynder/cae-fanout-svc.git
- git@github.com:Bynder/cae-metadata-reader-svc.git
- git@github.com:Bynder/cae-office-converter-svc.git
- git@github.com:Bynder/cae-pdf-converter-svc.git
- git@github.com:Bynder/cae-recognition-svc.git
- git@github.com:Bynder/cae-revamped-converter-svc.git
- git@github.com:Bynder/cae-svg-converter-svc.git
- git@github.com:Bynder/cae-video-converter-svc.git
- git@github.com:Bynder/video-event-handler-svc.git

## Process
If $ARGUMENTS is empty, then scan only the current folder else scan the specified folders.
for each folder start search for the following HTTP clients or Kafka consumers:

Always use V4 of the Pact specification.
use subagents where possible.

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

### Provider
For each provider register the following information
- clone the repository in /tmp dir, if the repository exists then make sure it is up to date master
- scan the app for which services are producing the messages that the kafka consumer is consuming.
- record the work thatis needed to implement the contract on the provider end. You will need to report this

## Output
Generate a report at `.pact/PACT_CONSUMER.md`.

### HTTP clients
For each HTTP consumer, use the template `@references/pact/http-template.md` and include:
- Folder
- Method
- Base URL
- Path
- Response type
- Properties used to create the contract
- A table row that maps each template column to the corresponding value
- The generated contract in JSON format directly below the table
- A third part that is agent-friendly and describes exactly what must be implemented on the consumer side in this repo (sufficient for planning-agent task creation)
- A fourth part that is agent-friendly and describes exactly what must be implemented on the provider side (sufficient for planning-agent task creation)

If required input is missing, ask the user.

### Kafka consumers
For each Kafka consumer, use the template `@references/pact/kafka-template.md` and include:
- Folder
- Consumer group name
- Topic
- Properties used to create the contract
- A table row that maps each template column to the corresponding value
- The generated contract in JSON format directly below the table
- A third part that is agent-friendly and describes exactly what must be implemented on the consumer side in this repo (sufficient for planning-agent task creation)
- A fourth part that is agent-friendly and describes exactly what must be implemented on the provider side (sufficient for planning-agent task creation)

If required input is missing, ask the user.

### Contract summary
Add a table with the following columns:
- Folder
- Total number of contracts

### Missing context/resources
List all resources or inputs that were needed but not provided, so better context can be supplied next time.

ask to create to tasks for the work that needs to be done on the consumer end and the provider end.
When confirmed create the tasks in markdown format in folder .pact/tasks with the following naming convention:
if it's consumer task:
Pact_Consumer_[servicename]_[messagename].md. Use the template @references/pact/task-template.md
else
Pact_Provider_[servicename]_TASK_N.md. Use the template @references/pact/task-template.md

