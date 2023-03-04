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
| Ali Asbai | 1h | 2h | 5 h | 45 m | 6 h | 4 h | 3 h | 2 h | 24 h |
| David Ljunggren | 1h | 1h | 8h | 1h | 6h | 5h | 1h | 1h | 24h |
| Christofer Vikström | 1h | 1h | 6h | 30m | 6h | 4h | 1h | 30m | 20h |

For setting up tools and libraries (step 4), enumerate all dependencies
you took care of and where you spent your time, if that time exceeds
30 minutes.

## Overview of issue 1

**Title:**  
Reduce priority levels and add confidence value.

**URL:**  
https://github.com/pmd/pmd/issues/4327

**Summary in one or two sentences:**  
Diffrent programming flaws and issues have diffrent severity levels depending on how deterimental they are to the overall software quality. PMD currently split the severity of the issues into 5 priority levels. But they want to decrease the priority levels to 3. Also they want to assign a confidence level to each reported issue.

**Scope (functionality and code affected):**  
Almost all files in the pmd-core folder aswell as 2 files in pmd-doc.

### Requirements for the new feature or requirements affected by functionality being refactored

| ID | Title | Description |
|---|---|---|
| 1 | Feature | The integers 1-5 need to map to three priority levels instead of 5. |
| 2 | Regression Testing | The rules that are in-place for all the supported languages need to continue working. |
| 3 | Regression Testing | All hardcoded tests must work without changing them |
| 4 | Regression Testing | Operations which should override aspects of rules continue to be tracked correctly. |
| 5 | Regression Testing | Operations which should not override underlying rules continue to be tracked correctly. |
| 6 | Coding Conventions | Any new code match the codestyle determined by the project. |
| 7 | Regression Testing | All tests succed and the project builds correctly. |

### Code changes

**Patch:** https://github.com/AliAsbai/pmd/pull/10/commits/0beac2168fb9c2b967a76abfa3d1e48a73dc5bcc  
First we removed the priority level between high and medium called medium_high. We acomplished this by changing the index 2 that was previously mapped to medium_high and made it map to medium instead. The index 3 that was mapped to medium preiously mapped to nothing for the time being. We replaced all cases of prioritty level medium_high in tests with either medium or high depending on what was best in each context. We also changed all instances of priority level 3 (old medium) with priority level 2 (new medium, old medium_high).

**Patch:** https://github.com/AliAsbai/pmd/pull/10/commits/1145f9b23404d5cc0c460f33b6fb9e88a5dbd127  
Secondly we removed the priority level between medium and low called medium_low. We acomplished this by changing the index 5 that was previously mapped to low and made it map to nothing instead. The index 3 was mapped to low instead. We replaced all cases of prioritty level medium_low in tests with either medium or high depending on what was best in each context. We also changed all instances of priority level 5 (old low) with priority level 3 (new low).

**Patch:** https://github.com/AliAsbai/pmd/pull/10/commits/b19848610fc47e966a9790fce9a8c35b5ee522a1  
We now modified the validation process of priority levels to only accept priority levels in the range 1-3 instead of 1-5.

**Patch:** https://github.com/AliAsbai/pmd/pull/10/commits/f2abc2b403258526ff2f621f20223136a47ef590  
Then we added some new tests that check that priority levels are validated corrctly in the right range and that each priority level is mapped to the correct index.

**Patch:** https://github.com/AliAsbai/pmd/pull/10/commits/605a82e2f15eeb14b7a1a01b89f9f64b434af10c  
The solution as it stood passed all tests old and new. But are over 20 packackges in the project for diffrent programmming languages each containing thousands of rules that were currently using the old indexes 1-5 for their priorirty levels. All of these would no longer work if our solution were commited to the main project. So this had to be fixed, since the rules are so many we saw it as virtually impossible to go through them all and change their values to comply with the new solution. Therefore we altered the solution. The priority levels medium and low now mapped to their old indexes 3 and 5 respectively. But now the indexes for the old priority levels medium_high and medium_low were alos mapped to priority levels medium and low respectively. So now index 1 mapped to priority level high, indexes 2 and 3 mapped to priority level medium and indexes 4 and 5 mapped to priority level low. Alot of tests had to be reverted to their old values before there were any changes and the validation process of priority levels was reverted to accept indexes 1-5 again. Now all the indexes mapped to 3 priority levels and all the tests were successful while all old rules continued to work as expected. We were done!

If you want to see the full timeline and changes of this issue you can find that in the issue tracker at https://github.com/AliAsbai/pmd/pull/10/commits

### Test results

These test results are from the file PMDPParametersTest.java, this file is responsible for testing what values constitute a valid priority level and what indexes map to which priority levels.

**Before**:  
![Tests Before](https://i.imgur.com/XBRR1Ui.png "Tests before refactoring")

We added some test that check that the valid range for priority level indexes are 1-5. We also added tests that check that each index 1-5 is mapped to the correct priority level.

**After:**  
![Tests After](https://i.imgur.com/sNlyv9Q.png "Tests after refactoring")

To see the full test results, you can access it by navigating to the following path in the web browser:

**Before refactoring:**
	
	test-results/Test Results - All_in_pmd-core_Before.html

**After refactoring:**

	test-results/Test Results - All_in_pmd-core_After.html

## Overview of issue 2

**Title:**  
Improve UseStringBufferForStringAppends to report on variable declaration.

**URL:** 
https://github.com/pmd/pmd/issues/4290

**Summary in one or two sentences:**  
Improve the UseStringBufferForStringAppends rule by making it report on variable declaration instead of on each concatenation.

**Scope (functionality and code affected):**  
UseStringBufferForStringAppendsRule class and test data: UseStringBufferForStringAppends.xml file.

### Requirements for the new feature or requirements affected by functionality being refactored

| ID | Title | Description |
|---|---|---|
| 1 | Feature | UseStringBufferForStringAppends rule should report on variable declaration instead of on each concatenation. |
| 2 | Regression Testing | All tests should be passed after modification. |
| 3 | Coverage | New tests should be added to increase the code coverage. |

### Code changes

**Patch:**
https://github.com/AliAsbai/pmd/pull/8/commits

### Test results

To see the test results, you can access it by navigating to the following path in the web browser:

**Before refactoring:**
	
	test-results/Test Results - UseStringBufferForStringAppendsTestBefore.html

**After refactoring:**

	test-results/Test Results - UseStringBufferForStringAppendsTestAfter.html

## Overview of issue 3

**Title:**  
Rename rule MethodArgumentCouldBeFinal to FormalParameterCouldBeFinal.

**URL:**  
https://github.com/pmd/pmd/issues/4287

**Summary in one or two sentences:**  
Rename the rule class/method to the requested name. Also changed the name of the test class/method for consistency reasons. 

**Scope (functionality and code affected):**  
No major functionality difference. 

### Requirements for the new feature or requirements affected by functionality being refactored

| ID | Title | Description |
|---|---|---|
| 1 | Refactoring | Rename the rule class/method to the requested name. |
| 2 | Refactoring | Change the name of the test class/method for consistency. |
| 3 | Regression Testing | The regression tests should pass after modification. |

### Code changes

**Patch:**
https://github.com/AliAsbai/pmd/pull/12/commits

### Test results

## Overview of issue 4

**Title:**  
Complete ConstantsInInterface hint to alternative location in enum.

**URL:**  
https://github.com/pmd/pmd/issues/1205

**Summary in one or two sentences:**  
Made changes to an error message, and to the PMD wiki. 

**Scope (functionality and code affected):**  
No major functionality difference. 

### Requirements for the new feature or requirements affected by functionality being refactored

| ID | Title | Description |
|---|---|---|
| 1 | Feature | The error message should be short and not be phrased as "Avoid ...". |
| 2 | Documentation | The Wiki should have a more detailed description which refers the programmer to the appropriate item in Effective Java. |
| 3 | Regression Testing | The regression tests should pass after modification. |

**Patch:**

_[This patch has been accepted, or at least been considered for acceptance by the project.](https://github.com/pmd/pmd/pull/4412)_

https://github.com/AliAsbai/pmd/pull/9/commits

### Test results

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

The main take-aways from the project were that working as unit, with a variety of different competences, is a real strength when working with such a large open source repository. As an individual, certain tasks or issues can seem quite unapproachable if they require much onboarding and topic specific knowledge, but as a team, larger issues were more approachable. One thing that the group learned while working on this project is how working on different projects comes with different policies and principles. How to contribute to a project can vary a lot and understanding how this translates to issue resolution (refactoring standards etc) and the ways of working was interesting as certain aspects from the previous assignments had to be adjusted to fit the current requirements and policies set by the administrators of the open source repository. 

How did you grow as a team, using the Essence standard to evaluate yourself?

To work as a team with issue resolution for a quite large open source repository required that individual responsibilities were formulated early in the project during planning. This meant that it should be clear for each team member how the tasks should be performed and establish channels for communication. Since the assignment required collaboration between members, the honest and open communication between members was encouraged so that potential individual problems could be tackled as a larger unit. How to measure the progress in the group was mainly done using communication channels and issue trackers on GitHub. When trying to identify feasible issues to resolve, efforts to mitigate wasted work was a priority but could sometimes slip through anyways as certain parts of issues were deemed unfeasible for the scope of the assignment only when complicated sub-issues could be identified while working on said issue. When situations like this occured, the problem was communicated, discussed and in one scenario (issue#2) the issue was deemed too vague in its description and unfeasible to complete within the time limit, leading to work being wasted trying to solve that specific issue. Since the communication within the group was open, the members of the team could trust that other members would reach out if any problems were encountered, and if nothing was communicated, that the members were working on solving their parts of the problems at hand. At the end of the project, the team could rely on each other for help if needed. 

**Optional (point 6): How would you put your work in context with best software engineering practice?**

We think it makes sense to mention the alpha "Work" from the kernel. A big setback for us was that we were stuck on step 2 (prepared) and 3 (started) for too long, which resulted in much less time for actual development. We were stuck on step 2 due to not finding suitable projects that everyone wanted to work on. At one point, we actually thought we had found a good project, but it turned out that it did not quite meet the assignments criteria, so after consulting with TAs and the examiner, we decided to switch projects a week before the deadline. Needless to say, it took quite some time to find a project that met all our requirements. On top of all the requirements set by the assignment itself, not only did we want the codebase to be in Java, but we also wanted the product to be something that we would consider using, because we find it hard to work on stuff that we do not care for. 

When we had decided on the PMD project, it took quite a long time before we considered the work to go "well" (step 4), and we were thus stuck on step 3. Finding issues that we could resolve given the limited time, while also not being too trivial, was not easy. At this stage, we realized that the majority of our time would go to reading documentation and analyzing code. We also realized that it does not always make sense to collaborate on issues, because it is sometimes difficult to subdivide issues into smaller tasks, which often leads to duplicating work and effort. We think the requirements system is a great way of making it easier to collaborate on issues, however, and we think we managed to use this system rather neatly.

We have also come to the conclusion that the Opportunity / Stakeholder alphas play a large role for the developers as well. Reason being, we feel like it is quite difficult to maintain the motivation needed to develop and contribute towards open source projects without having a clear background of the bigger picture. Just solving a bug for a project which perhaps will not live to see itself being deployed is rather demotivating. 

Optional (point 7): Is there something special you want to mention here?
