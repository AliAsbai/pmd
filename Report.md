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
| Ali Asbai |  |  | 4 h | 45 m | 6 h | 4 h | 3 h | 2 h | 20 h |
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

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Issue:**  
https://github.com/pmd/pmd/issues/4290

**Patch:**
https://github.com/AliAsbai/pmd/pull/8/commits

## Test results

To see the test results, you can access it by navigating to the following path in the web browser:

**Issue:**  
https://github.com/pmd/pmd/issues/4327

**Before refactoring:**
	
	test-results/Test Results - All_in_pmd-core_Before.html

**After refactoring:**

	test-results/Test Results - All_in_pmd-core_After.html

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Issue:**  
https://github.com/pmd/pmd/issues/4290

**Before refactoring:**
	
	test-results/Test Results - UseStringBufferForStringAppendsTestBefore.html

**After refactoring:**

	test-results/Test Results - UseStringBufferForStringAppendsTestAfter.html

## UML class diagram and its description

![UML Diagram](https://github.com/AliAsbai/pmd/blob/5-write-the-report/uml.png "UML Diagram")

Partial UML diagram over the system, with more detailed focus in the area most affected by issue https://github.com/pmd/pmd/issues/4327.

### Key changes/classes affected

For issue https://github.com/pmd/pmd/issues/4327 most of the work was done in the Rule interface, the RuleReference class and the RulePriority class. Work was also dont in the Abstractrule and AbstractRenderer subclasses which there were too many of to list in the UML diagram. Alot of work was also done in improving and creating new tests for all classes in the pmd-core package.

### Architectural overview

PMD is a static code analysis tool that helps developers improve the quality of their Java code by identifying potential issues, coding violations, and other problems that could impact the performance and maintainability of their applications. The tool works by analyzing the source code of a application and applying a set of predefined rules to the codebase. 

Using PMD can help developers identify and fix issues early in the development process, before they become more costly and time-consuming to address. By improving the quality of their code, developers can also improve the performance, maintainability, and overall reliability of their applications.

The PMD architecture is based on a modular framework that is easily extendible. At its core, the PMD architecture consists of three main components: parsers, a rule module, and a reporting module.

The parsers are responsible for converting source code into an abstract syntax tree (AST) that can be used by the rule module to analyze the code by applying predefined rules that the code is supposed to follow. Because of the projects open-source nature and the modular framework developers can easily create custom parsers to support other languages or frameworks.

The rule module is responsible for applying a set of predefined rules to the AST and flag if any issues are detected. PMD includes a wide range of rules that cover various aspects of code quality, such as complexity, readability, maintainability, and performance. Developers can also create custom rules to meet their specific needs.

Finally, the reporting module is responsible for generating reports on the results of the analysis. PMD supports multiple report formats, including HTML, XML, and CSV.

Since the rule module is one of the core features of the application, our changes had an impact on all other modules of the application. This made it extremely important that we refractored the code in a way that did not change how the rest of the application communicates with the rule module.

Optional (point 2): relation to design pattern(s).

## Overall experience

What are your main take-aways from this project? What did you learn?

How did you grow as a team, using the Essence standard to evaluate yourself?

**Optional (point 6): How would you put your work in context with best software engineering practice?**

We think it makes sense to mention the alpha "Work" from the kernel. A big setback for us was that we were stuck on step 2 (prepared) and 3 (started) for too long, which resulted in much less time for actual development. We were stuck on step 2 due to not finding suitable projects that everyone wanted to work on. At one point, we actually thought we had found a good project, but it turned out that it did not quite meet the assignments criteria, so after consulting with TAs and the examiner, we decided to switch projects a week before the deadline. Needless to say, it took quite some time to find a project that met all our requirements. On top of all the requirements set by the assignment itself, not only did we want the codebase to be in Java, but we also wanted the product to be something that we would consider using, because we find it hard to work on stuff that we do not care for. 

When we had decided on the PMD project, it took quite a long time before we considered the work to go "well" (step 4), and we were thus stuck on step 3. Finding issues that we could resolve given the limited time, while also not being too trivial, was not easy. At this stage, we realized that the majority of our time would go to reading documentation and analyzing code. We also realized that it does not always make sense to collaborate on issues, because it is sometimes difficult to subdivide issues into smaller tasks, which often leads to duplicating work and effort. We think the requirements system is a great way of making it easier to collaborate on issues, however, and we think we managed to use this system rather neatly.

We have also come to the conclusion that the Opportunity / Stakeholder alphas play a large role for the developers as well. Reason being, we feel like it is quite difficult to maintain the motivation needed to develop and contribute towards open source projects without having a clear background of the bigger picture. Just solving a bug for a project which perhaps will not live to see itself being deployed is rather demotivating. 

Optional (point 7): Is there something special you want to mention here?
