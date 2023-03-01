# Report for assignment 4

This is a template for your report. You are free to modify it as needed.
It is not required to use markdown for your report either, but the report
has to be delivered in a standard, cross-platform format.

## Project

**Name:** PMD

**URL:** https://github.com/pmd/pmd

**One or two sentences describing it:** "PMD is a source code analyzer. It finds common programming flaws like unused variables, empty catch blocks, unnecessary object creation, and so forth."



## Onboarding experience

**Did you choose a new project or continue on the previous one?**

We chose a new project since the one we used for assignment 3 was a collection of algorithms, which is not acceptable for this assignment.

**If you changed the project, how did your experience differ from before?**

Unlike the previous project, this project has a very smooth onboarding process. It is not difficult to set up the environment and start working on the project after reading the README file.


## Effort spent

For each team member, how much time was spent:

| Team member | Plenary discussions/meetings | Discussions within parts of the group | Reading documentation | Configuration and setup | Analyzing code/output | Writing documentation | writing code | running code | Total |
| ------------- | ---------------------------- | ---------------------------------- | ------------------ | -------------------- | ------------------- | --------------- | --------------- | ----------- | ----- |
| Ouday Ahmed |  |  |  |  |  |  |  |  |  |
| Martin Arenbro |  |  |  |  |  |  |  |  |  |
| Ali Asbai |  |  |  |  |  |  |  |  |  |
| David Ljunggren |  |  |  |  |  |  |  |  |  |
| Christofer Vikström |  |  |  |  |  |  |  |  |  |

For setting up tools and libraries (step 4), enumerate all dependencies
you took care of and where you spent your time, if that time exceeds
30 minutes.

## Overview of issue(s) and work done.

**Title:**  
Reduce priority levels and add confidence value.

**URL:**  
https://github.com/pmd/pmd/issues/4327

**Summary in one or two sentences:**  
Diffrent programming flaws and issues have diffrent severity levels depending on how deterimental they are to the overall software quality. PMD currently split the severity of the issues into 5 priority levels. But they want to decrease the priority levels to 3. Also they want to assign a confidence level to each reported issue.

**Scope (functionality and code affected):**  
Almost all files in the pmd-core folder aswell as 2 files in pmd-doc.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Title:**  
Improve UseStringBufferForStringAppends to report on variable declaration.

**URL:**  
https://github.com/pmd/pmd/issues/4290

**Summary in one or two sentences:**  
Improve the UseStringBufferForStringAppends rule by making it report on variable declaration instead of on each concatenation.

**Scope (functionality and code affected):**  
UseStringBufferForStringAppendsRule class and test data: UseStringBufferForStringAppends.xml file.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Title:**  
Rename rule MethodArgumentCouldBeFinal to FormalParameterCouldBeFinal.

**URL:**  
https://github.com/pmd/pmd/issues/4287

**Summary in one or two sentences:**  
Rename the rule class/method to the requested name. Also changed the name of the test class/method for consistency reasons. 

**Scope (functionality and code affected):**  
No major functionality difference. 
## Requirements for the new feature or requirements affected by functionality being refactored

**Issue:**  
https://github.com/pmd/pmd/issues/4327

**Requirements:**
- The integers 1-5 need to map to three priority levels instead of 5.
- The rules that are in-place for all the supported languages of PMD need to continue to work without changing them.
- All hardcoded test rules need to continue to work without changing them (unless it is to improve the test).
- Operations which should override aspects of rules continue to be tracked correctly.
- Operations which should not override underlying rules continue to be tracked correctly.
- Any new code match the codestyle determined by the project.
- All tests succed and the project builds correctly.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Issue:**  
https://github.com/pmd/pmd/issues/4290

**Requirements:**
- UseStringBufferForStringAppends rule should report on variable declaration instead of on each concatenation.
- All tests should be passed after modification.
- New tests should be added to increase the code coverage.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Issue:**  

**Requirements:**

## Code changes

### Patch

**Issue:**  
https://github.com/pmd/pmd/issues/4327

**Patch:**
https://github.com/AliAsbai/pmd/pull/10/commits

**Issue:**  
https://github.com/pmd/pmd/issues/4290

**Patch:**
https://github.com/AliAsbai/pmd/pull/8/commits

## Test results

To see the test results, you can access it by navigating to the following path in the web browser:

**Issue:**  
https://github.com/pmd/pmd/issues/4290

**Before refactoring:**
	
	test-results/Test Results - UseStringBufferForStringAppendsTestBefore.html

**After refactoring:**

	test-results/Test Results - UseStringBufferForStringAppendsTestAfter.html

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

## UML class diagram and its description

### Key changes/classes affected

Optional (point 1): Architectural overview.

Optional (point 2): relation to design pattern(s).

## Overall experience

What are your main take-aways from this project? What did you learn?

How did you grow as a team, using the Essence standard to evaluate yourself?

Optional (point 6): How would you put your work in context with best software engineering practice?

Optional (point 7): Is there something special you want to mention here?
