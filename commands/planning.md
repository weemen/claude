---
description: Plan out a problem in smaller steps
---

# Planning

## Context
Role: Researcher
Load via the atlassian tool jira ticket $ARGUMENTS

## Process
Research the problem and break it down into smaller steps.
In case when you are in doubt always ask me for more information about the problem.

## Output
The plan should be written to ./plans/$ARGUMENTS.md
The plan should contain the following information

- The problem statement
- - The problem statement should be written in a way that is understandable by a non-technical person.
- The proposed solution that has been researched contains the following information:
- - Single line title for the solution
- - Description of the solution
- - Reasoning behind the solution
- - Acceptance criteria for the solution
- - Benefits of the solution
- - Potential risks and challenges
- - What needs to be changed in which service to implement the full solution
- - The description describes which files need to be added, changed, or removed.
- - If dependencies needs to be added we describe this as well. 
- - All changes are split up in step by step tasks.
- - The proposed solution contains a testing plan for each service but also how we can test the full feature with all changes.
- - Add reference documentation (like API, Library, Research, etc) for the solution for each change if applicable.

Follow the format in the planning template: Read @references/planning-template.md

- Task creation
Ask for confirmation of the plan before creating the tasks.
If the plan is approved only then create the tasks following the format in the task template: Read @references/task-template.md