---
description: Plan out a problem in smaller steps
---

# Planning

## Context
Role: Researcher
Load via the atlassian tool jira ticket $ARGUMENTS
The jira ticket number will be used as the name of the plan.

## Process
### 1. Analyze Existing Codebase Patterns

Search for similar implementations:
- Look for comparable features or components
- Identify relevant files and their structure
- Note patterns, conventions, and standards used
- Document reusable code or utilities

### 2. Research External Documentation

If needed, search for:
- Framework best practices
- Library documentation
- Design patterns
- Similar implementations

### 3. Design Implementation Approach

Determine:
- Which files need to be created or modified
- What models/schemas are required
- Which services or utilities are needed
- How this integrates with existing code
- What testing strategy to use

### 4. Break Down Into Tasks

Create detailed, actionable tasks with:
- Specific file paths
- Exact function/class names
- Clear acceptance criteria
- Validation commands

## Output
The plan should be written to ./plans/$ARGUMENTS.md
The plan should contain the following information

- The problem statement
- - The problem statement should be written in a way that is understandable by a non-technical person.
- The proposed solution that has been researched contains the following information:
- - Single line title for the solution
- - Description of the solution
- - Reasoning behind the solution
- - Why we chose this approach over alternatives
- - Key technical decisions and trade-offs
    **Approach Decision:**
    We chose [approach name] because:
- [Reason 1]
- [Reason 2]
- [Reason 3]

**Alternatives Considered:**
- [Alternative 1]: Rejected because [reason]
- [Alternative 2]: Rejected because [reason]
- - How this integrates with existing architecture]
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
If the plan is approved only then:
- if the jira ticket is an epic create the user stories for the epic
- if the jira ticket is not an epic then create sub-tasks for the jira ticket
- create the tasks following the format in the task template: Read @references/task-template.md
