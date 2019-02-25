# Report for assignment 4

This is a template for your report. You are free to modify it as needed.
It is not required to use markdown for your report either, but the report
has to be delivered in a standard, cross-platform format.

## Project

Name: Apache Samza

URL: https://github.com/apache/samza

Apache Samza is a distributed stream processing framework. It is a scalable data processing engine that allows
 you to process and analyze your data in real-time. 
    
## Architectural overview and purpose of the system (optional, as one item for P+)
Samza is a data-processing engine that is scalable. The purpose of Samza is that it allows the user to analyze and process the data in real time via streams in a fast non costly way. A stream is simply put a bunch or a collection of messages that cannot be changed. Often the messages are of the same type, or at least in the same category. Streams in Samza can have many people writing to a stream or many people reading from a stream at the same time. Streams are divided into different partitions. When a stream receives a message, the message is distributed to one of the streams partitions. Every message that is distributed to a partition has a unique offset so that each message can uniquely can be identified. Samza could be used for both stateful and stateless data processing. Simply put, stateful processing is when you need to save some state or record of a message after it has been processed in the stream and stateless processing is the opposite when you do not have to keep a record of a state after a message has been processed. Samza has a processing guarantee, which means that each message that enters a stream will be processed at least once. This guarantees that every message will be read, even if there are failures.

Samza uses distributed execution. It first breaks down the application in multiple tasks, each task takes data from one partition of the input streams and the assignment of partitions never change. The task is restarted somewhere else if the machine that the task is on fails, and the task still consumes the same stream partitions. Samza allows tasks to execute independent of each other without sharing any state since there is no ordering of messages across partitions.

![alt text](http://samza.apache.org/img/1.0.0/learn/documentation/architecture/task-assignment.png)

Each 	application also has a coordinator which manages the assignment of tasks. The coordinator makes sure that machines are working properly and redistributes tasks if it fails.  

Samza has a very flexible threading model to run each task, you can control the number of workers needed to process your data as well as the number of threads each worker uses to to run its tasks. Each thread can run one or more tasks and tasks don't share any state, thus you don’t have to worry about coordination across threads.

Samza also guarantees that even if your job crashes, the machine dies, there is a network fault, messages won’t be lost. This is done by having each task periodically persisting the last processed offsets for its input partitions. 

Each Samza task is associated with its own instance of a local database (state-store) which allows tasks to be relocated without affecting the overall application. 

Sources
* http://samza.apache.org/learn/documentation/1.0.0/core-concepts/core-concepts.html
* http://samza.apache.org/learn/documentation/1.0.0/architecture/architecture-overview.html

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
