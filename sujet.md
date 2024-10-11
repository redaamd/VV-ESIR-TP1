# Practical Session #1: Introduction

1. Find in news sources a general public article reporting the discovery of a software bug. Describe the bug. If possible, say whether the bug is local or global and describe the failure that manifested its presence. Explain the repercussions of the bug for clients/consumers and the company or entity behind the faulty program. Speculate whether, in your opinion, testing the right scenario would have helped to discover the fault.

2. Apache Commons projects are known for the quality of their code and development practices. They use dedicated issue tracking systems to discuss and follow the evolution of bugs and new features. The following link https://issues.apache.org/jira/projects/COLLECTIONS/issues/COLLECTIONS-794?filter=doneissues points to the issues considered as solved for the Apache Commons Collections project. Among those issues find one that corresponds to a bug that has been solved. Classify the bug as local or global. Explain the bug and the solution. Did the contributors of the project add new tests to ensure that the bug is detected if it reappears in the future?

3. Netflix is famous, among other things we love, for the popularization of *Chaos Engineering*, a fault-tolerance verification technique. The company has implemented protocols to test their entire system in production by simulating faults such as a server shutdown. During these experiments they evaluate the system's capabilities of delivering content under different conditions. The technique was described in [a paper](https://arxiv.org/ftp/arxiv/papers/1702/1702.05843.pdf) published in 2016. Read the paper and briefly explain what are the concrete experiments they perform, what are the requirements for these experiments, what are the variables they observe and what are the main results they obtained. Is Netflix the only company performing these experiments? Speculate how these experiments could be carried in other organizations in terms of the kind of experiment that could be performed and the system variables to observe during the experiments.

4. [WebAssembly](https://webassembly.org/) has become the fourth official language supported by web browsers. The language was born from a joint effort of the major players in the Web. Its creators presented their design decisions and the formal specification in [a scientific paper](https://people.mpi-sws.org/~rossberg/papers/Haas,%20Rossberg,%20Schuff,%20Titzer,%20Gohman,%20Wagner,%20Zakai,%20Bastien,%20Holman%20-%20Bringing%20the%20Web%20up%20to%20Speed%20with%20WebAssembly.pdf) published in 2018. The goal of the language is to be a low level, safe and portable compilation target for the Web and other embedding environments. The authors say that it is the first industrial strength language designed with formal semantics from the start. This evidences the feasibility of constructive approaches in this area. Read the paper and explain what are the main advantages of having a formal specification for WebAssembly. In your opinion, does this mean that WebAssembly implementations should not be tested? 

5.  Shortly after the appearance of WebAssembly another paper proposed a mechanized specification of the language using Isabelle. The paper can be consulted here: https://www.cl.cam.ac.uk/~caw77/papers/mechanising-and-verifying-the-webassembly-specification.pdf. This mechanized specification complements the first formalization attempt from the paper. According to the author of this second paper, what are the main advantages of the mechanized specification? Did it help improving the original formal specification of the language? What other artifacts were derived from this mechanized specification? How did the author verify the specification? Does this new specification removes the need for testing?

## Answers
**Introduction :** 
This practical session will review some real software bugs, different techniques for fault tolerance, and the importance of testing. By investigating a series of examples from Apache Commons, Netflix, and WebAssembly, we learn how companies handle software bugs and ensure system reliability.

1. A serious software bug has been detected in the Mercedes-Benz electric cars, which affected the propelling of its EQS and EQE electric vehicles. This bug caused the electric drivetrain to lose propulsion suddenly and made the movement of the vehicle dangerous. Following reports of two such incidents, Mercedes launched a recall of over 8,000 vehicles in the U.S. It involved a software bug in the drivetrain plug connector that, under certain conditions, may cause the propulsion system to shut down without warning. The bug did not cause any injuries or crashes but triggered a massive recall.
The bug is global in nature, affecting multiple variants of EVs across the Mercedes-Benz lineup. The failure, when it happens, is manifested by the vehicle suddenly losing its motive power, which definitely heightens the risk of an accident, a lot more so whenever traveling at high speeds or in heavy traffic. 
The carmaker has planned an update to the software as a response to prevent further occurrences.
For Mercedes-Benz, this could erode consumer confidence in the brand and, more specifically, their still growing roster of EVs. The consumer equates it with aggravation and a possible safety issue where the affected vehicles need to be brought back into the dealers for a software fix. 
In our opinion, testing under various real-world conditions and, more specifically, with specific plug connector interactions, may have helped detect the issue at an earlier stage of its development.
[Click here to view the article](https://www.carscoops.com/2023/06/mercedes-recalls-eqs-and-eqe-evs-for-software-bug-that-could-cause-sudden-power-loss/)



2. The bug in this collection-729 'Add test case to IteratorUtilsTest' is to add test cases in class `IteratorUtilsTest` for covering various scenarios of different iterator types and functions. In detail, the focus will be on methods like `nodeListIterator`, `asEnumeration`, `pushbackIterator`, etc., where null input should throw an appropriate exception-a `NullPointerException` or `IllegalArgumentException`.
These tests were contributed by several different contributors with the intent of catching any future changes or regressions regarding null inputs or the handling of specific iterator functions at the test level. The mere fact that it contains `@Test(expected=NullPointerException.class)` and similar patterns enforces handling those edge cases and its detection if the bug reappears.
This bug was rather local in that it mainly addressed input validation problems in the IteratorUtils class. Extra tests are added to guarantee that when these functions would be updated in the future or modified, mistakes would be found early during testing. 
here is an example sample of the code : 

![example](https://github.com/user-attachments/assets/4b926fe0-e799-45de-8b62-a466c4ee2fe6)


3. The paper outlines several concrete experiments that Netflix conducts regularly as part of their Chaos Engineering. Here's a brief overview based on the document presented:

**Concrete Experiments :** 
Chaos Monkey: This internal service randomly terminates virtual machine instances hosting production services to ensure that services can survive instance failures. It runs when people are at work-that is, during regular working hours-so that engineers are around to respond rapidly to any issues popping up.
Chaos Kong: Simulates the failure of an entire Amazon EC2 region, further testing the resiliency of the system against larger-scale failures.
Failure Injection Testing FIT: Intentional request failures between services within Netflix let the team confirm that the system gracefully degrades during a failure condition.

**Requirements for Experiments :** 
Steady State Definition: Define an output measure indicating the normal state of the system.
Hypothesis Formulation: A hypothesis should be formulated based on what one expects as a steady state behavior of the experiment. 
**Realistic Variables:** 
The experiments should introduce real life events that may affect the performance of the system, such as server crashes or network failures. Production Environment: Run experiments in the production environment so that one can assess and observe real user impact on the system behavior. 

**Variables Observed :**
Steady State Metrics: For example, SPS will be constantly monitored as part of efforts towards the quantification of the impact brought about by the introduction of faults. To that effect, it is ensured that the system is available to the users to deliver content before and after these experiments are conducted. It also includes the general user experience, including the deterioration in the quality of service. 

**Primary Outcomes :** the primary results that were obtained from this experiment, include the following:
 A hike in the level of confidence about the system's ability to deal with failure.
Understanding how the different parts of the system interact when they are under stress.
Resilience in an engineering culture that designs services with failure in mind.

**Other Companies Running Similar Experiments :**
Chaos Engineering is not peculiar to Netflix. Other companies, like Amazon, Google, Microsoft, and Facebook, have done similar things to test the resilience of their systems. It does point to a greater recognition of the importance of fault tolerance in today's modern software development.

**Speculation on Implementation in Other Organizations :**
Other organizations can do similar experiments by doing the following:
Determining Critical Services: It would include pinpointing those services that are vital to their operations and which can only afford to have a minimal amount of failure.
Introducing Artificial Failures: Implementing tools like Chaos Monkey, that randomly kill services or simulate network failures.
Key Metric Monitoring: These would include the response times, error rates, and user engagement observed during such experiments to measure the impact of the artificially induced failures.
Iterative Testing: Regular execution of experiments and automation of such, in order to adapt to changes in the system over time. By adopting these practices, organizations can increase the resilience of their systems, making sure they remain available even in the case of unplanned failures.


4. The major advantages of WebAssembly's formal specification are :


**Clarity and precision**: A formal specification gives in clear detail the syntax and semantics of the language. Therefore, developers have an idea of how WebAssembly should behave. This cuts down ambiguity and misinterpretation during implementation.


**Soundness and Correctness**: Formal specifications allow proof of soundness to be done for the implementation, as it adheres to defined semantics.


**Facilitates Optimization**: A well-defined formal specification will let compiler developers optimize their implementation much better, knowing what exactly the language is going to behave like.


**Interoperability**: A formal specification ensures that different WebAssembly implementations, say different browsers, behave uniformly.


**Ease of Verification**: Formal specifications can be used to verify that implementations behave as expected. This should bring most bugs and inconsistencies out early in the development process.


So, in our opinion, while a formal specification enhances the reliability and understanding of WebAssembly, comprehensive testing remains a very important component in practice, ensuring robustness and performance.



5. The author has listed several benefits of the mechanized specification of WebAssembly:


**Eyeball Closeness:** The mechanization conveys "eyeball closeness," meaning there is a line-by-line correspondence between the official specification and the mechanized version. 


This, in fact, makes it more understandable to people who knew the original specification as if it were some sort of pseudocode representation of the specification. 


**Soundness Proof:** This paper presents a fully mechanized soundness proof for the WebAssembly type system. The proof was useful not only to check the type system, but also during the development of this specification, when it uncovered several problems.


**Other Artifacts:** The mechanized specification thus yields a verified executable interpreter and a verified type checker. These artifacts are crucial in the validation of the mechanized specification to ensure that it really behaves as expected. 


**Validation by Testing:** This specification has been tested using the official WebAssembly conformance test suite and differential fuzzing against major WebAssembly engines. This allows us, for instance, to validate that a mechanized specification is correct as well as an interpreter derived through,.


All in all, the author does not say that removes the need for testing. The mechanized specification supplements testing in that it puts a formal basis on which bugs can be found out and correctness can be established. One is not to pass over testing, since it is also an integral part in the process of development-a great way for bugs to be found out that might not be as easily observed from purely formal proofs.




**Conclusion :**
This session demonstrates the importance of testing and verification in software development, showing that even with formal specifications, testing remains crucial for maintaining software quality and performance.










