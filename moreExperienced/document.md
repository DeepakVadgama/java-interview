#### 1. difference between s3 and ec2?
- Amazon EC2 (Elastic Computing Cloud) : That is cloud web service solution, which can be used for hosting your application. Basically EC2 is like a huge computer machine which runs either Windows or Linux (or any other OS). And is capable of handling whatever software or application you install on it.
- Amazon S3 (Simple Storage Service) : While S3 is more a data storage solution/service. This is typically used to store large binary files or other important data. You can compare S3 system with a huge hard-disk, where any amount of data can be stored and accessed, with very less I/O overheads (As it is designed for handling billions of data objects). 
- Amazon also has other storage and database services, like RDS for relational databases and DynamoDB for NoSQL.

#### 2. what type of service is used to connec backend to front end?
- Server-rendered apps:
The first is straight up HTTP requests to a server-rendered app. This is a system whereby the browser sends a HTTP request and the server replies with a HTML page.
Between receiving the request and responding, the server usually queries the database and feeds it into a template (ERB, Blade, EJS, Handlebars).
Once the page is loaded in the browser, HTML defines what things are, CSS how they look and JS any special interactions.
- Communication using AJAX: AJAX stands for Asynchronous JavaScript and XML. This means that the JavaScript loaded in the browser sends a HTTP request (XHR, XML HTTP Request) from within the page and historically got a XML response.
- We’re now building backend services that don’t even run all the time, just when they’re required, thanks to serverless architectures like AWS Lambda.

#### 3. verical and horizontal scaling aws?
- Vertical Scaling:
For the initial users up to 100, a single EC2 instance would be sufficient, e.g. t2.micro/t2.nano. The one instance would run the entire web stack, for example, web app, database, management, etc. The original architecture is fine until your traffic ramps up. Here you can scale vertically by increasing the capacity of your EC2 instance to address the growing demands of the application when the users grow up to 100.
- Horizontal Scaling:
Horizontal scaling essentially involves adding machines in the pool of existing resources. When users grow up to 1000 or more, vertical scaling can’t handle requests and horizontal scaling is required. Horizontal scalability can be achieved with the help of clustering, distributed file system, and load balancing.
Loosely coupled distributed architecture allows for scaling of each part of the architecture independently. This means a group of software products can be created and deployed as independent pieces, even though they work together to manage a complete workflow. Each application is made up of a collection of abstracted services that can function and operate independently. This allows for horizontal scaling at the product level as well as the service level.
- How To Achieve Effective Horizontal Scaling::
The first is to make your application stateless on the server side as much as possible. Any time your application has to rely on server-side tracking of what it’s doing at a given moment, that user session is tied inextricably to that particular server. If, on the other hand, all session-related specifics are stored browser-side, that session can be passed seamlessly across literally hundreds of servers. The ability to hand a single session (or thousands or millions of single sessions) across servers interchangeably is the very epitome of horizontal scaling.
The second goal to keep square in your sights is to develop your app with a service-oriented architecture. The more your app is comprised of self-contained but interacting logical blocks, the more you’ll be able to scale each of those blocks independently as your use load demands. Be sure to develop your app with independent web, application, caching and database tiers. This is critical for realizing cost savings – because, without this microservice architecture, you’re going to have to scale up each component of your app to the demand levels of the services tier getting hit the hardest.
- vertical - scale up
- horizontal - scale out

#### 4. T2 instances are a new low-cost, General Purpose instance type that are designed to provide a baseline level of CPU performance with the ability to burst above the baseline. T2 instances are designed to provide moderate baseline performance and the capability to burst to higher performance as required by workload.

#### 5.  relationship between instance and AMI?
- An Amazon Machine Image (AMI) is an encrypted machine image of a specific computer running an operating system that is configured in a specific way and that can also contain a set of applications and services for accomplishing a specific purpose. An AMI contains all the information necessary to start up and run the software in the image. 
Think of an EC2 instance as a single running server with CPU, memory, hard disk, networking, etc. Any changes you make to that instance affect only that instance.
Think of an AMI (Amazon Machine Image) as an exact copy of the root file system that gets copied to the hard disk when you start a new instance. The AMI is a hard disk sitting on a shelf. You make an exact copy of the hard disk on the shelf, install the new hard disk in a server, and turn the server on. You can do this for as many servers as you'd like to start without affecting the master copy.

#### 6. what are the key components of AWS?

- The key components of AWS are
- Route 53: A DNS web service
- Simple E-mail Service: It allows sending e-mail using RESTFUL API call or via regular SMTP
- Identity and Access Management: It provides enhanced security and identity management for your AWS account
- Simple Storage Device or (S3): It is a storage device and the most widely used AWS service
- Elastic Compute Cloud (EC2): It provides on-demand computing resources for hosting applications. It is very useful in case of unpredictable workloads
- Elastic Block Store (EBS): It provides persistent storage volumes that attach to EC2 to allow you to persist data past the lifespan of a single EC2
- CloudWatch: To monitor AWS resources, It allows administrators to view and collect key Also, one can set a notification alarm in case of trouble.

#### 7. Difference betwwen spring mvc and spring boot?
- Spring MVC is a complete HTTP oriented MVC framework managed by the Spring Framework and based in Servlets. It would be equivalent to JSF in the JavaEE stack. The most popular elements in it are classes annotated with @Controller, where you implement methods you can access using different HTTP requests. It has an equivalent @RestController to implement REST based APIs.
- Spring boot is a utility for setting up applications quickly, offering an out of the box configuration in order to build Spring powered applications. As you may know, Spring integrates a wide range of different modules in its umbrella, as spring-core, spring-data, spring-web (which includes Spring MVC, by the way) and so on. With this tool you can tell Spring how many of them to use and you'll get a fast setup for them (you are allowed to change it by yourself later on).
- So, Spring MVC is a framework to be used in web applications and Spring boot is a Spring based production-ready project initializer.

#### 8. Lazy loading and lazy fetching?
- Say you have a parent and that parent has a collection of children. Hibernate now can "lazy-load" the children, which means that it does not actually load all the children when loading the parent. Instead, it loads them when requested to do so. You can either request this explicitly or, and this is far more common, hibernate will load them automatically when you try to access a child.
- "Lazy loading" means that an entity will be loaded only when you actually accesses the entity for the first time.
- Lazy fetching decides whether to load child objects while loading the Parent Object. You need to do this setting respective hibernate mapping file of the parent class.


#### 10. http verbs:
- The POST verb is most-often utilized to **create** new resources. In particular, it's used to create subordinate resources. That is, subordinate to some other (e.g. parent) resource. In other words, when creating a new resource, POST to the parent and the service takes care of associating the new resource with the parent, assigning an ID (new resource URI), etc.
On successful creation, return HTTP status 201, returning a Location header with a link to the newly-created resource with the 201 HTTP status.
POST is neither safe nor idempotent
- The HTTP GET method is used to **read** (or retrieve) a representation of a resource. In the “happy” (or non-error) path, GET returns a representation in XML or JSON and an HTTP response code of 200 (OK). In an error case, it most often returns a 404 (NOT FOUND) or 400 (BAD REQUEST).
- PUT is most-often utilized for **update** capabilities, PUT-ing to a known resource URI with the request body containing the newly-updated representation of the original resource.
However, PUT can also be used to create a resource in the case where the resource ID is chosen by the client instead of by the server. In other words, if the PUT is to a URI that contains the value of a non-existent resource ID
- PATCH is used for **modify** capabilities. The PATCH request only needs to contain the changes to the resource, not the complete resource.
- DELETE is pretty easy to understand. It is used to **delete** a resource identified by a URI.
On successful deletion, return HTTP status 200 (OK) along with a response body, perhaps the representation of the deleted item (often demands too much bandwidth), or a wrapped response (see Return Values below). Either that or return HTTP status 204 (NO CONTENT) with no response body. In other words, a 204 status with no body, or the JSEND-style response and HTTP status 200 are the recommended responses.


#### 11.  What is Exception Handling?
- Exception Handling is a mechanism to handle runtime errors.
- 1) Checked Exception
The classes that extend Throwable class except RuntimeException and Error are known as checked exceptions e.g.IOException, SQLException etc. Checked exceptions are checked at compile-time.

2) Unchecked Exception
The classes that extend RuntimeException are known as unchecked exceptions e.g. ArithmeticException, NullPointerException, ArrayIndexOutOfBoundsException etc. Unchecked exceptions are not checked at compile-time rather they are checked at runtime.

3) Error
Error is irrecoverable e.g. OutOfMemoryError, VirtualMachineError, AssertionError etc.


#### 12. by default how many buckets will be there at AWS?
- 0. By default, you can create up to 100 buckets in each of your AWS accounts

#### 13. explain flow of things when user clicks ui to backend?
- https://www.quora.com/How-do-front-end-and-back-end-technologies-work-together

#### 14. TDD test driven development
- TDD is an iterative software development process where you first write the test with the idea that it must fail. This is a different approach to the traditional development where you write the application functionality first and then write test cases.
- 
EJB 3.0 Interview Questions
Test Driven Development Interview Questions

What is Test Driven Development (TDD) ?
TDD is an iterative software development process where you first write the test with the idea that it must fail. This is a different approach to the traditional development where you write the application functionality first and then write test cases. The major benefit of this approach is that the code becomes thoroughly unit tested (you can use JUnit or other unit testing frameworks). TDD is based on two important principles preached by its originator Kent Beck:
Write new business code only if an automated unit test has failed: Business application requirements drive the tests and tests drive the actual functional code. Each test should test only one business concept, which means avoid writing a single test which tests withdrawing money from an account and depositing money into an account. Any change in the business requirements will impact pre and post conditions of the test. Talking about pre and post conditions, following design by contract methodology helps achieving TDD. In design by contract, you specify the pre and post conditions that act as contracts of a method, which provides a specification to write your tests against.
Eliminate duplication from the code: A particular business concept should be implemented only once within the application code. Code for checking an account balance should be centralized to only one place within the application code. This makes your code decoupled, more maintainable and reusable. I can hear some of you all saying how can we write the unit test code without the actual application code. Let's look at how it works in steps. The following steps are applied iteratively for business requirements.
STEP: 1
write some tests for a specific business requirement.
STEP: 2
write some basic structural code so that your test compiles but the test should fail (failures are the pillars of success). For example just create the necessary classes and corresponding methods with skeletal code.
STEP: 3
write the required business code to pass the tests which you wrote in step 1.
STEP: 4
finally refactor the code you just wrote to make it is as simple as it can be. You can refactor your code with confidence that if it breaks the business logic then you have unit test cases that can quickly detect it.
STEP: 5
run your tests to make sure that your refactored code still passes the tests.

#### What is the point of Test Driven Development (TDD) ? What do you think of TDD ?
- TDD process improves your confidence in the delivered code for the following reasons.
- TDD can eliminate duplication of code and also disciplines the developer to focus his mind on delivering what is absolutely necessary. This means the system you develop only does what it is supposed to do because you first write test cases for the business requirements and then write the required functionality to satisfy the test cases and no more.
- These unit tests can be repeatedly run to alert the development team immediately if someone breaks any existing functionality. All the unit tests can be run overnight as part of the deployment process and test results can be emailed to the development team.
- TDD ensures that code becomes thoroughly unit tested. It is not possible to write thorough unit tests if you leave it to the end due to deadline pressures, lack of motivation etc.
- When using TDD, tests drive your code and to some extent they assist you in validating your design at an earlier stage.
- TDD also helps you refactor your code with confidence that if it breaks the business logic it gets picked up when you run your unit tests next time.
- TDD promotes design to interface not implementation design concept. 

#### Automatic dirty checking?
- Hibernate uses a strategy called inspection, which is basically this: when an object is loaded from the database a snapshot of it is kept in memory. When the session is flushed Hibernate compares the stored snapshot with the current state. If they differ the object is marked as dirty and a suitable SQL command is enqueued. If the object is still transient then it is always dirty.

#### Automatic Json validate?
``` java
public static void main( String[] args ) throws IOException, ProcessingException
{
    File schemaFile = new File("/Users/XYZ/schema.json");
    File jsonFile = new File("/Users/XYZ/data.json");
    	
    if (ValidationUtils.isJsonValid(schemaFile, jsonFile)){
    	System.out.println("Valid!");
    }else{
    	System.out.println("NOT valid!");
    }
}
```
- using jacksson library

#### what is cors?
- Cross-Origin Resource Sharing (CORS) is a mechanism that uses additional HTTP headers to let a user agent gain permission to access selected resources from a server on a different origin (domain) than the site currently in use. A user agent makes a cross-origin HTTP request when it requests a resource from a different domain, protocol, or port than the one from which the current document originated.

#### Stringbuilder or buffer?
- StringBuffer is synchronized, StringBuilder is not.
- StringBuilder is faster than StringBuffer because it's not synchronized.

#### What is countdown latch?
- CountDownLatch is used to make sure that a task waits for other threads before it starts.
- When we create an object of CountDownLatch, we specify the number of threads it should wait for, all such thread are required to do count down by calling CountDownLatch.countDown() once they are completed or ready to the job. As soon as count reaches zero, the waiting task starts running.
- https://www.geeksforgeeks.org/countdownlatch-in-java/
-  once count reaches zero you cannot use CountDownLatch any more


#### joint point vs point cu
- Pointcut: a predicate that matches join points. A point cut is something that defines at what join points an advice should be applied

These spring interview Questions are not very difficult in nature and focused on spring fundamentals rather than focusing on advanced feature of session management, sprint security, authentication etc. we will cover of those question on some other interview article. I would also suggest that share some spring questions asked to you guys during interview and then I can put together those with their answers for quick reference of everybody.

When you go out to a restaurant, you look at a menu and see several options to choose from. You can order one or more of any of the items on the menu. But until you actually order them, they are just “opportunities to dine”. Once you place the order and the waiter brings it to your table, it’s a meal.

- Join points are the options on the menu and pointcuts are the items you select. A joinpoint is an opportunity within code for you to apply an aspect…just an opportunity. Once you take that opportunity and select one or more joinpoints and apply an aspect to them, you’ve got a pointcut.

#### CI/CD pipeline
- continuous integration and deployment
- Continuous Integration can be defined as “Building software and taking it through as many tests as possible with every change”.
- What steps are in continuous integration? More steps in continuous integration means more stability.
Compilation
Unit Tests
Code Quality Gates
Integration Tests
Deployment
Chain Tests

#### how can you improve performance of web app?
- https://stackify.com/java-performance/


#### what is microservice architecture? why companies are moving to microservice? how to deploy on aws?
- Microservices are an architectural and organizational approach to software development where software is composed of small independent services that communicate over well-defined APIs. These services are owned by small, self-contained teams.
- With monolithic architectures, all processes are tightly coupled and run as a single service. This means that if one process of the application experiences a spike in demand, the entire architecture must be scaled.
- With a microservices architecture, an application is built as independent components that run each application process as a service. These services communicate via a well-defined interface using lightweight APIs. Services are built for business capabilities and each service performs a single function. 
- While its natural for new companies to take the monolithic-first approach because its quick and you can deploy quickly as well, over time, as the monolith gets bigger, breaking it down into microservices becomes the most convenient solution.
- you create separate code for serives and deploy on aws using elastic load balancer by uploading the war file.

#### what are the important spring security parameters hat you should follow?
- How does Spring Security Authentication work? Here are a few steps to know.

The user logs in with a name (username or email) and a password. These two credentials are combined into an instance of the class UsernamePasswordAuthenticationToken (which is itself an instance of the Authentication interface). Then, they’re passed to the AuthenticationManager for verification.
If the password does not match the username, the BadCredentialsException is returned along with the message “Bad Credentials.”
If the password and username match, it will return a populated Authentication instance.
The user sets a security context by calling the SecurityContextHolder.getContext () method setAuthentication (…), where the object that returned the AuthenticationManager is passed.
- https://www.upwork.com/hiring/development/spring-security-framework/

#### Types of transactional management in spring
-   Spring supports two types of transaction management:

 Programmatic transaction management : This means that you have to manage the transaction with the help of programming. That gives you extreme flexibility, but it is difficult to maintain.

 Declarative transaction management: This means you separate transaction management from the business code. You only use annotations or XML based configuration to manage the transactions.
 - https://dzone.com/articles/spring-transaction-management
 

#### custom exception in java?
- class NoSuchProductException extends RuntimeException 
