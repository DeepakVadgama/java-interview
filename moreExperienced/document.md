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

#### 9. how can you improve performance of web app?
- 


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


