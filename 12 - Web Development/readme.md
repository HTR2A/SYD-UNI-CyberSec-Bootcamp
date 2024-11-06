# Cybersecurity Bootcamp - Module 12: Web Development Quiz

## In this Challenge, I reviewed many of the concepts and tools that I learned in the Web Development module.

### Question 1

**What type of architecture does the HTTP request and response process occur in?**

- **Answer**: HTTP uses client-server architecture.
- **Problem**: Understanding the architecture that underpins web communication.
- **What I Learned**: I learned that HTTP operates using a client-server architecture, where clients send requests and servers provide responses.

### Question 2

**What are the different parts of an HTTP request?**

- **Answer**: The request line, the request headers, and an optional request body.
- **Problem**: Identifying the components of an HTTP request.
- **What I Learned**: I learned that an HTTP request consists of a request line, headers, and sometimes a request body that contains additional data.

### Question 3

**Which part of an HTTP request is optional?**

- **Answer**: The request body.
- **Problem**: Understanding the optional parts of an HTTP request.
- **What I Learned**: I learned that the request body is optional and is used primarily in methods like POST to send additional data.

### Question 4

**What are the three parts of an HTTP response?**

- **Answer**: The status line, the response headers, and the response body.
- **Problem**: Understanding the structure of an HTTP response.
- **What I Learned**: I learned that an HTTP response includes a status line indicating the outcome, headers with metadata, and an optional body with content.

### Question 5

**Which number class of status codes represent errors?**

- **Answer**: 400 and 500.
- **Problem**: Identifying which status codes indicate errors.
- **What I Learned**: I learned that 400-level status codes represent client errors, while 500-level codes represent server errors.

### Question 6

**What are the two most common request methods a security professional encounters?**

- **Answer**: GET and POST requests.
- **Problem**: Knowing which HTTP methods are most common.
- **What I Learned**: I learned that GET and POST are the most frequently used HTTP methods, with GET used for retrieving data and POST for sending data.

### Question 7

**Which type of HTTP request method is used for sending data?**

- **Answer**: POST.
- **Problem**: Determining which method is used for sending data.
- **What I Learned**: I learned that the POST method is used to send data to a server, commonly used in forms and APIs.

### Question 8

**What are the advantages of using curl over the browser?**

- **Answer**: It allows you to easily see the response status lines, is repeatable, can be automated, and can be edited while in use.
- **Problem**: Understanding the benefits of using curl for web requests.
- **What I Learned**: I learned that curl is advantageous for testing and automation because it provides direct access to response details, can be repeated easily, and can be integrated into scripts.

### Question 9

**Which curl option is used to change the request method?**

- **Answer**: -X.
- **Problem**: Learning how to modify the request method in curl.
- **What I Learned**: I learned that the `-X` option in curl is used to specify the HTTP method, such as GET, POST, or PUT.

### Question 10

**Which curl option is used to set request headers?**

- **Answer**: -H.
- **Problem**: Understanding how to add headers to a request using curl.
- **What I Learned**: I learned that the `-H` option in curl allows you to set custom headers, which is useful for specifying content types and authentication details.

### Question 11

**Which request method might an attacker use to figure out which HTTP requests an HTTP server will accept?**

- **Answer**: OPTIONS.
- **Problem**: Understanding potential security vulnerabilities.
- **What I Learned**: I learned that the OPTIONS method can be used to determine which HTTP methods are allowed on a server, which could help an attacker identify potential attack vectors.

### Question 12

**Which response header sends a cookie to the client?**

- **Answer**: Set-Cookie.
- **Problem**: Identifying the HTTP header responsible for managing cookies.
- **What I Learned**: I learned that the `Set-Cookie` header is used by servers to send cookies to clients, which can be stored and sent back with subsequent requests.

### Question 13

**What is the request method in the following HTTP request example?**

```
POST /login.php HTTP/1.1
Host: example.com
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Type: application/x-www-form-urlencoded
Content-Length: 34
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Linux; Android 6.0; Nexus 5 Build/MRA58N) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.132 Mobile Safari/537.36
username=Barbara&password=password
```

- **Answer**: POST.
- **Problem**: Identifying the request method from an HTTP request.
- **What I Learned**: I learned how to identify the HTTP request method by looking at the first line of the request.



### Question 14

**Which header expresses the client's preference for an encrypted response?**

```
POST /login.php HTTP/1.1
Host: example.com
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Type: application/x-www-form-urlencoded
Content-Length: 34
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Linux; Android 6.0; Nexus 5 Build/MRA58N) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.132 Mobile Safari/537.36

username=Barbara&password=password
```

- **Answer**: Upgrade-Insecure-Requests: 1.
- **Problem**: Understanding headers that indicate security preferences.
- **What I Learned**: I learned that the `Upgrade-Insecure-Requests` header is used by clients to indicate that they prefer a secure, encrypted connection.



### Question 15

**What is the response status code in the following HTTP response example?**

```
HTTP/1.1 200 OK
Date: Mon, 16 Mar 2020 17:05:43 GMT
Last-Modified: Sat, 01 Feb 2020 00:00:00 GMT
Content-Encoding: gzip
Expires: Fri, 01 May 2020 00:00:00 GMT
Server: Apache
Set-Cookie: SessionID=5
Content-Type: text/html; charset=UTF-8
Strict-Transport-Security: max-age=31536000; includeSubDomains
X-Content-Type: NoSniff
X-Frame-Options: DENY
X-XSS-Protection: 1; mode=block
```

- **Answer**: 200.
- **Problem**: Understanding how to identify the status of an HTTP response.
- **What I Learned**: I learned that the response status code is a numeric value indicating the result of an HTTP request, with 200 representing a successful request.

### Question 16

**What are the individual components of microservices called?**

- **Answer**: Services.
- **Problem**: Understanding how microservices are organized.
- **What I Learned**: I learned that microservices are composed of individual components called services, each responsible for a specific function.

### Question 17

**What is a service that writes to a database and communicates to other services?**

- **Answer**: An application programming interface (API).
- **Problem**: Understanding services that handle data and communication in web development.
- **What I Learned**: I learned that an API can be used as a service to write to databases and communicate with other services, playing a key role in data-driven applications.

### Question 18

**What tool can be used to deploy multiple containers at once?**

- **Answer**: Docker Compose.
- **Problem**: Learning about tools for container orchestration.
- **What I Learned**: I learned that Docker Compose is a tool that allows developers to define and deploy multiple Docker containers simultaneously, which is useful for managing multi-container applications.

### Question 19

**What kind of file format is required for us to deploy a container set?**

- **Answer**: YAML.
- **Problem**: Understanding the configuration formats used in container deployment.
- **What I Learned**: I learned that Docker Compose uses YAML files to define the services, networks, and volumes needed for container deployment, providing an easy-to-read configuration format.

### Question 20

**Which type of SQL query would we use to see all the information in a table called customers?**

- **Answer**: SELECT \* FROM customers;
- **Problem**: Understanding SQL queries for retrieving data.
- **What I Learned**: I learned that the `SELECT * FROM customers` query is used to retrieve all records and fields from the `customers` table in a database.

### Question 21

**Which type of SQL query would we use to enter new data into a table?**

- **Answer**: INSERT INTO.
- **Problem**: Understanding SQL commands for adding data to a table.
- **What I Learned**: I learned that the `INSERT INTO` statement is used to add new records to a table in a database, specifying the table and the values to be inserted.

