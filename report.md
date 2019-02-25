# Report for assignment 4

This is a template for your report. You are free to modify it as needed.
It is not required to use markdown for your report either, but the report
has to be delivered in a standard, cross-platform format.

## Project

Name: Apache Samza

URL: https://github.com/apache/samza

Apache Samza is a distributed stream processing framework. It is a scalable data processing engine that allows
 you to process and analyze your data in real-time. 
    
## Architectural overview (optional, as one item for P+)

## Selected issue(s)

Title: Refactor TaskContextImpl to not include access to objects that are only used internally

URL: https://issues.apache.org/jira/browse/SAMZA-1935

TaskContext should be a public API but TaskContextImpl is being used to pass around objects for internal use. Some 
internal components cast TaskContext to a TaskContextImpl to access these objects, which is not ideal.

## Onboarding experience

The onboarding documentation is actually very good in this project and can be found in the README.md. We did not have to search for information on a different place to be able to build the project and run tests using gradle.
Gradle was a required tool to build the project. The project specified commands for building the project using gradle as well as where to download gradle if you don’t have it on your local machine.

Samza integrates with YARN for dependency management and running stream-processing as a managed service. Samza works with YARN to distribute resources and it also handles failures of individual instances and automatically restarts them. And scala is a programming language that combines an object oriented approach and functional programming into one high level programming language.

The build as well as the tests conclude without any errors.


## Requirements affected by functionality being refactored

We need to split up the internal functionality by creating a separate object which is only passed around internally 
and is decoupled from TaskContextImpl.

## Existing test cases relating to refactored code

## The refactoring carried out

(Link to) a UML diagram and its description

## Test logs

Overall results with link to a copy of the logs (before/after refactoring).

The refactoring itself is documented by the git log.

## Effort spent

For each team member, how much time was spent in

* Viktor 
    1. plenary discussions/meetings;
    
    2. discussions within parts of the group;
    
    3. reading documentation;
    
    4. configuration;
    
    5. analyzing code/output;
    
    6. writing documentation;
    
    7. writing code;
    
    8. running code?
    
* Cyril 
    1. plenary discussions/meetings;
    
    2. discussions within parts of the group;
    
    3. reading documentation;
    
    4. configuration;
    
    5. analyzing code/output;
    
    6. writing documentation;
    
    7. writing code;
    
    8. running code?
    
* Robin 
    1. plenary discussions/meetings;
    
    2. discussions within parts of the group;
    
    3. reading documentation;
    
    4. configuration;
    
    5. analyzing code/output;
    
    6. writing documentation;
    
    7. writing code;
    
    8. running code?
    
* Sara 
    1. plenary discussions/meetings;
    
    2. discussions within parts of the group;
    
    3. reading documentation;
    
    4. configuration;
    
    5. analyzing code/output;
    
    6. writing documentation;
    
    7. writing code;
    
    8. running code?
    
* Fredrik 
    1. plenary discussions/meetings;
    
    2. discussions within parts of the group;
    
    3. reading documentation;
    
    4. configuration;
    
    5. analyzing code/output;
    
    6. writing documentation;
    
    7. writing code;
    
    8. running code?

## Overall experience

What are your main take-aways from this project? What did you learn?

Is there something special you want to mention here?
