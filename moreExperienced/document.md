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

