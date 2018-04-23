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

#### 7. 
