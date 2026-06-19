# create_global_rules command for a project
This command creates global rules for a project. 
Global rules are rules that apply to all files in a project, regardless of their location.
The global rules are stored in AGENTS.md file.

## Context
Role: Expert Software Engineer
Global rules are rules that apply to all files in a project, regardless of their location.
The global rules are stored in AGENTS.md file.

## Process
Create an AGENTS.md file if this file does not exist yet. 
If the already AGENTS.md file exists, stop what you are doing.  
If the project is not empty, then create a global rules file based on the code in the project.
If the project is empty then ask for the tech stack and generate the global rules file.

The global rules file should contain the following:
- The project overview
- The core principles of the project: which describe things like TYPE SAFETY, KISS, YAGNI apply to every line of code
- The architecture of the project: how should features be vertically sliced. 
- Documentation style: how should documentation be written. All code needs to be documented consistently
- Logging Rules: how should logging be done in the project. Which logging library should be used, what information should be logged, and how should logs be structured.
- Development Workflow Commands: which commands should be used for development, testing, and deployment. This can include commands for running the application, running tests, and deploying to production.
- Testing Structure: All code needs tests, mirroring structure is critical
- Committable code: All code needs to be formatted, linted and all tests need to pass before a commit can be made.

The global rules file should be stored in the project root directory.
The global rules file may contain examples
The global rules file does not contain more than 500 lines
The global rules file is concise and easy to read 

## Output
The global rules file is created and tell me where I can find the file.
