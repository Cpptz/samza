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
Before the refactoring a Context object was given as input and called getTaskContext upon which returned a TaskContext object. This object wa then casted to a TaskContextImpl object to be able to use a couple of methods which did not even fit into the TaskContextImpl class. A new class, called JobContextMetaData was created, with some of the attributes and methods from the TaskContextImpl class. The attributes JobModel, StreamMetadataCache and Map<String, Object>, and the methods registerObject and fetchObject were moved. The methods getJobModel and getStreamMetadataCache were only copied and moved to the JobContextMetadata class, since the methods were needed to create a Context object. 

After the refactoring the init method takes a Context object and a JobContextMetadata object as input, creates a TaskContext object from the context but uses it for less calls than before. Now the JobContextMetadata object is used when calling fetchObject and getStreamMetadataCache instead. The major difference however is that the TaskContext object received when calling getTaskContext on the Context object does not have to be casted to a TaskContextImpl object.


### Before
![](./images/before_class.png)


![](./images/before_seq.png)


### After
![](./images/after_class.png)


![](./images/after_seq.png)


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
Finding a suitable project that seemed doable was not a trivial task. After finding the Samza project and building it, understanding the project and the requirements of the refactoring was quite a challenge. We spent a lot of time as a group discussing how to best approach the problem and if our proposed solutions would work. We learnt that a seemingly trivial refactoring problem could in fact be much harder than it looked in the beginning. More time that expected was spent trying to find a solution without any code being written. Furthermore we learned that additional dependencies could be found within our project which would further complicate the refactoring. The experience of the given documentation was overall good, for example it was easy to build the project based on the documentation in the README.md. If anything was unclear, additional information could be found on their website: http://samza.apache.org/ 
We reached out to the community of the project in order to register as an assignee and within a day we were able to connect with the issue reporter (Cameron Lee). He seemed glad that we showed interest in the project and referred to Yi Pan who was able to register us on the project. The conversation can be found in the comment section: https://issues.apache.org/jira/browse/SAMZA-1935

What are your main take-aways from this project? What did you learn?
Is there something special you want to mention here?

Fredrik:

Viktor:

Sara:

Cyril:

Robin:

