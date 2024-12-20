# CURL

[Curl](https://www.kali.org/tools/curl/) is a command-line tool for transferring data with URL syntax. It supports DICT, FILE, FTP, FTPS, GOPHER, HTTP, HTTPS, IMAP, IMAPS, LDAP, LDAPS, POP3, POP3S, RTMP, RTSP, SCP, SFTP, SMTP, SMTPS, TELNET, and TFTP.

Curl supports SSL certificates, HTTP POST, HTTP PUT, FTP uploading, HTTP form-based upload, proxies, cookies, user+password authentication (Basic, Digest, NTLM, Negotiate, Kerberos…), file transfer resume, proxy tunneling, and a busload of other useful tricks.

## HyperText Transfer Protocol (HTTP)

Today, the majority of our applications, both web and mobile, constantly interact with the Internet. Most Internet communications are made with web requests through the HTTP protocol. HTTP is an application-level protocol used to access World Wide Web resources. Hypertext means text containing links to other resources and text that readers can easily interpret.

HTTP communication consists of a client and a server, where the client requests the server for a resource. The server processes the requests and returns the requested resource. The default port for HTTP communication is port 80, which can be changed to any other port, depending on the web server configuration. The exact requests are utilized when visiting different websites on the internet. We enter a Fully Qualified Domain Name (FQDN) as a Uniform Resource Locator (URL) to reach the desired website.

## URL

Resources over HTTP are accessed via a URL, which offers many more specifications than simply specifying a website we want to visit. Let's look at the structure of a URL: 

![image](https://github.com/user-attachments/assets/d83bd7d8-e960-4cff-a51e-1b9123ce6a5e)

Here is what each component stands for:

| Component    | Example           | Description                                                                                                                                                                     |
|--------------|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Scheme       | http:// https://  | This is used to identify the protocol being accessed by the client and ends with a colon and a double slash (://)                                                               |
| User Info    | admin:password@   | This is an optional component that contains the credentials (separated by a colon :) used to authenticate to the host and is separated from the host with an at sign (@)        |
| Host         | inlanefreight.com | The host signifies the resource location. This can be a hostname or an IP address                                                                                               |
| Port         | :80               | The Port is separated from the Host by a colon (:). If no port is specified, http schemes default to port 80, and HTTPS default to port 443                                     |
| Path         | /dashboard.php    | This points to the resource accessed as a file or a folder. If no path is specified, the server returns the default index (e.g., index.html).                                   |
| Query String | ?login=true       | The query string starts with a question mark (?) and consists of a parameter (e.g., login) and a value (e.g., true). Multiple parameters can be separated by an ampersand (&).  |
| Fragments    | #status           | The browsers on the client side process fragments to locate sections within the primary resource (e.g., a header or section on the page).                                       |

Not all components are required to access a resource. The main mandatory fields are the scheme and the host, without which the request would have no resources to request.

## HTTP Flow

![image](https://github.com/user-attachments/assets/dbfe3bf7-55f6-4c8d-aae5-e55efb02d3e5)

The diagram above presents the anatomy of an HTTP request at a very high level. The first time a user enters the URL (inlanefreight.com) into the browser, it requests a DNS (Domain Name Resolution) server to resolve the domain and get its IP. The DNS server looks up the IP address for inlanefreight.com and returns it. All domain names must be resolved this way, as a server can't communicate without an IP address.

> **Note**: Our browsers usually first look up records in the local `/etc/hosts` file, and if the requested domain does not exist within it, they will contact other DNS servers. We can use the `/etc/hosts` to manually add records for DNS resolution by adding the IP followed by the domain name.

Once the browser gets the IP address linked to the requested domain, it sends a GET request to the default HTTP/S port (e.g., 80/443), asking for the root/path. The web server then receives the request and processes it. By default, servers are configured to return an index file when a request for / is received.

In this case, the contents of index.html are read and returned by the web server as an HTTP response. The response also contains the status code (e.g., 200 OK), indicating the request was successfully processed. The web browser then renders the index.html contents and presents it to the user.

## Hypertext Transfer Protocol Secure (HTTPS)

One significant drawback of HTTP is that all data is transferred in clear text. This means anyone between the source and destination can perform a Man-in-the-middle (MITM) attack to view the transferred data.

The HTTPS (HTTP Secure) protocol was created to counter this issue. In this protocol, all communications are transferred in an encrypted format, so even if a third party intercepts the request, they cannot extract the data. For this reason, HTTPS has become the mainstream scheme for websites on the Internet. HTTP is being phased out, and most web browsers will soon not allow visiting HTTP websites.

## HTTPS Overview

If we examine an HTTP request, we can see the effect of not enforcing secure communications between a web browser and a web application. For example, the following is the content of an HTTP login request:

![image](https://github.com/user-attachments/assets/77761f60-dfac-40e1-a6d9-d745674ada7a)

The login credentials are visible in clear text. This would make it easy for someone on the same network (such as a public wireless network) to capture the request and reuse the credentials for malicious purposes.

In contrast, when someone intercepts and analyzes traffic from an HTTPS request, they would see something like the following:

![image](https://github.com/user-attachments/assets/bf1233cc-12ee-4965-9252-87814965fdbb)

As we can see, the data is transferred as a single encrypted stream, which makes it very difficult for anyone to capture information such as credentials or any other sensitive data.

> **Note**: Although the data transferred through the HTTPS protocol may be encrypted, the request may still reveal the visited URL if it contacts a clear-text DNS server. For this reason, it is recommended to utilize encrypted DNS servers (e.g., 8.8.8.8 or 1.1.1.1) or a VPN service to ensure all traffic is adequately encrypted.


### HTTPS Flow

Let's look at how HTTPS operates at a high level:

![image](https://github.com/user-attachments/assets/f567d9cb-9b3e-4cda-8d0b-b8ac43482afa)

If we type http:// instead of https:// to visit a website that enforces HTTPS, the browser attempts to resolve the domain and redirects the user to the web server hosting the target website. A request is sent to port 80 first, which is the unencrypted HTTP protocol. The server detects this and redirects the client to secure HTTPS port 443 instead. This is done via the 301 Moved Permanently response code, which we will discuss in an upcoming section.

Next, the client (web browser) sends a "client hello" packet containing information about itself. The server replies with "server hello," followed by a key exchange to exchange SSL certificates. The client verifies the key/certificate and sends one of its own. After this, an encrypted handshake is initiated to confirm whether the encryption and transfer are working correctly.

Once the handshake is complete successfully, HTTP communication continues, and it is encrypted after that. This is a very high-level overview of the key exchange.

> **Note**: Depending on the circumstances, an attacker may be able to perform an HTTP downgrade attack, which downgrades HTTPS communication to HTTP, making the data transferred in clear text. This is done by setting up a Man-In-The-Middle (MITM) proxy to transfer all traffic through the attacker's host without the user's knowledge. However, most modern browsers, servers, and web applications protect against this attack.

## HTTP Requests and Responses

HTTP communications mainly consist of an HTTP request and an HTTP response. An HTTP request is made by the client (e.g., cURL/browser) and is processed by the server (e.g., web server). The requests contain all the details we require from the server, including the resource (e.g., URL, path, parameters), any request data, headers or options we specify, and many other options we will discuss throughout this module.

Once the server receives the HTTP request, it processes it and sends the HTTP response containing the response code, as discussed in a later section. It may also include the resource data if the requester can access it.

### HTTP Request

Let's start by examining the following example HTTP request:

![image](https://github.com/user-attachments/assets/88e2aaa0-affc-41ee-9044-f030295b6085)

The image above shows an HTTP GET request to the URL:

```URL
http://inlanefreight.com/users/login.html
```

The first line of any HTTP request contains three main fields 'separated by spaces':

| Field   | Example           | Description                                                                                                         |
|---------|-------------------|---------------------------------------------------------------------------------------------------------------------|
| Method  | GET               | The HTTP method or verb specifies the action type to perform.                                                       |
| Path    | /users/login.html | The path to the resource being accessed. This field can also be suffixed with a query string (e.g. ?username=user). |
| Version | HTTP/1.1          | The third and final field denotes the HTTP version.                                                                 |

The next set of lines contains HTTP header value pairs, like `Host`, `User-Agent`, `Cookie`, and many other possible headers. These headers are used to specify various attributes of a request. The headers are terminated with a new line, which is necessary for the server to validate the request. Finally, a request may end with the request body and data.

> **Note**: HTTP version 1.X sends requests as clear text and uses a new-line character to separate different fields and requests. On the other hand, HTTP version 2.X sends requests as binary data in a dictionary form.

### HTTP Response

Once the server processes our request, it sends its response. The following is an example HTTP response:

![image](https://github.com/user-attachments/assets/ac08b2f9-8dd9-4ed9-8b37-e377fa713a74)

The first line of an HTTP response contains two fields separated by spaces. The first is the HTTP version (e.g., HTTP/1.1), and the second denotes the HTTP response code (e.g., 200 OK).

Response codes are used to determine the request's status, as will be discussed later. After the first line, the response lists its headers, similar to an HTTP request. Both request and response headers are discussed in the next section.

Finally, the response may end with a response body, separated by a new line after the headers. The response body is usually defined as HTML code. However, it can also respond with other code types such as JSON, website resources such as images, style sheets, or scripts, or even a document such as a PDF document hosted on the webserver.

## HTTP Headers

HTTP headers pass information between the client and the server. Some headers are only used with either requests or responses, while some other general headers are standard to both. Headers can have one or multiple values, appended after the header name and separated by a colon. We can divide headers into the following categories:

1. General Headers
2. Entity Headers
3. Request Headers
4. Response Headers
5. Security Headers

### General Headers

[General headers](https://www.w3.org/Protocols/rfc2616/rfc2616-sec4.html) are used in HTTP requests and responses. They are contextual and **describe the message rather than its contents.**

| Header     | Example                             | Description                                                                                                                                                                                                                                                                                                                                                                       |
|------------|-------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Date       | Date: Wed, 16 Feb 2022 10:38:44 GMT | Holds the date and time the message originated. It's preferred to convert the time to the standard [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time) zone.                                                                                                                                                                                                          |
| Connection | Connection: close                   | Dictates if the current network connection should stay alive after the request finishes. Two commonly used values for this header are `close` and `keep-alive`. The client or server's `close` value means they would like to terminate the connection, while the `keep-alive` header indicates that the connection should remain open to receive more data and input.            |


### Entity Headers

Like general headers, [Entity Headers](https://www.w3.org/Protocols/rfc2616/rfc2616-sec7.html) can be standard to both the request and response. These headers **describe the content (entity) transferred by a message**. They are usually found in responses and POST or PUT requests.

| Header           | Example                     | Description                                                                                                                                                                                                                                                                                                 |
|------------------|-----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Content-Type     | Content-Type: text/html     | Used to describe the type of resource being transferred. The value is automatically added by the browsers on the client side and returned in the server response. The `charset` field denotes the encoding standard, such as [UTF-8](https://en.wikipedia.org/wiki/UTF-8).                                  |
| Media-Type       | Media-Type: application/pdf | The `media-type` is similar to `Content-Type`, and describes the transferred data. This header can be crucial in making the server interpret our input. The `charset` field may also be used with this header.                                                                                              |
| Boundary         | boundary="b4e4fbd93540"     | Acts as a marker to separate content when there is more than one in the same message. For example, within a form data, this boundary gets used as `--b4e4fbd93540` to separate different form parts.                                                                                                        |
| Content-Length   | Content-Length: 385         | Holds the size of the entity being passed. This header is necessary as the server uses it to read data from the message body, and the browser and tools like cURL automatically generate it.                                                                                                                |
| Content-Encoding | Content-Encoding: gzip      | Data can undergo multiple transformations before being passed. For example, large amounts of data can be compressed to reduce the message size. The type of encoding should be specified using the `Content-Encoding` header.                                                                               |

### Request Headers

The client sends [Request Headers](https://tools.ietf.org/html/rfc2616) in an HTTP transaction. These headers are used in an HTTP request and do not relate to the content of the message. The following headers are commonly seen in HTTP requests.

| Header        | Example                                | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|---------------|----------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Host          | Host: www.inlanefreight.com            | Used to specify the host being queried for the resource. This can be a domain name or an IP address. HTTP servers can be configured to host different websites, which are revealed based on the hostname. This makes the host header an important enumeration target, as it can indicate the existence of other hosts on the target server.                                                                                                                        |
| User-Agent    | User-Agent: curl/7.77.0                | The `User-Agent` header describes the client requesting resources. This header can reveal a lot about the client, such as the browser, version, and operating system.                                                                                                                                                                                                                                                                                               |
| Referer       | Referer: http://www.inlanefreight.com/ | Denotes where the current request is coming from. For example, clicking a link from Google search results would make `https://google.com` the referer. Trusting this header can be dangerous as it can be easily manipulated, leading to unintended consequences.                                                                                                                                                                                         |
| Accept        | Accept: */*                            | The `Accept` header describes which media types the client can understand. It can contain multiple media types separated by commas. The `*/*` value signifies that all media types are accepted.                                                                                                                                                                                                                                                                    |
| Cookie        | Cookie: PHPSESSID=b4e4fbd93540         | Contains cookie-value pairs in the format `name=value`. A [cookie](https://en.wikipedia.org/wiki/HTTP_cookie) is a piece of data stored on the client and server, which acts as an identifier. These are passed to the server per request, thus maintaining the client's access. Cookies can also serve other purposes, such as saving user preferences or session tracking. There can be multiple cookies in a single header separated by a semi-colon.         |
| Authorization | Authorization: BASIC cGFzc3dvcmQK      | Another method for the server to identify clients. After successful authentication, the server returns a token unique to the client. Unlike cookies, tokens are stored only on the client side and retrieved by the server per request. Multiple authentication types are based on the web server and application type used.                                                                                                                                      |

A complete list of request headers and their usage can be found [here](https://tools.ietf.org/html/rfc7231#section-5).


### Response Headers

[Response Headers](https://tools.ietf.org/html/rfc7231#section-7) can be **used in an HTTP response and do not relate to the content**. Specific response headers such as Age, Location, and Server provide more context about the reaction. The following headers are commonly seen in HTTP responses.

| Header           | Example                                   | Description                                                                                                                                                                               |
|------------------|-------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Server           | Server: Apache/2.2.14 (Win32)             | Contains information about the HTTP server that processed the request. It can be used to gain information about the server, such as its version, and enumerate it further.                |
| Set-Cookie       | Set-Cookie: PHPSESSID=b4e4fbd93540        | Contains the cookies needed for client identification. Browsers parse the cookies and store them for future requests. This header follows the same format as the `Cookie` request header. |
| WWW-Authenticate | WWW-Authenticate: BASIC realm="localhost" | Notifies the client about the authentication required to access the requested resource.                                                                                                   |


### Security Headers

Finally, we have [Security Headers](https://owasp.org/www-project-secure-headers/). With the increase in the variety of browsers and web-based attacks, it was necessary to define specific headers that enhanced security. HTTP Security headers are **a class of response headers used to specify particular rules and policies** the browser must follow while accessing the website.

| Header                    | Example                                     | Description                                                                                                                                                                                                                                                                                                                           |
|---------------------------|---------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Content-Security-Policy   | Content-Security-Policy: script-src 'self'  | Dictates the website's policy towards externally injected resources. This could be JavaScript code as well as script resources. This header instructs the browser to accept resources only from certain trusted domains, preventing attacks such as [Cross-site scripting (XSS)](https://en.wikipedia.org/wiki/Cross-site_scripting). |
| Strict-Transport-Security | Strict-Transport-Security: max-age=31536000 | Prevents the browser from accessing the website over the plaintext HTTP protocol and forces all communication to be carried over the secure HTTPS protocol. This prevents attackers from sniffing web traffic and accessing protected information such as passwords or other sensitive data.                                          |
| Referrer-Policy           | Referrer-Policy: origin                     | Dictates whether the browser should include the value specified via the `Referer` header. It can help avoid disclosing sensitive URLs and information while browsing the website.                                                                                                                                                     |

> **Note**: This section only mentions a small subset of commonly seen HTTP headers. Many other contextual headers can be used in HTTP communications. It's also possible for applications to define custom headers based on their requirements. A complete list of standard HTTP headers can be found [here](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers).


## HTTP Methods and Codes

HTTP supports multiple methods for accessing a resource. In the HTTP protocol, several request methods allow the browser to send information, forms, or files to the server. These methods are used, among other things, to tell the server how to process the request we send and how to reply.

We saw different HTTP methods used in the HTTP requests we tested in the previous sections. With cURL, if we use `-v` to preview the entire request, the first line contains the HTTP method (e.g., `GET / HTTP/1.1`), while with browser dev tools, the HTTP method is shown in the `Method` column. Furthermore, the response headers also contain the HTTP response code, which states the status of processing our HTTP request.

### Request Methods

The following are some of the commonly used methods:

| Method  | Description                                                                                                                                                                                                                                                                                                                               |
|---------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| GET     | Requests a specific resource. Additional data can be passed to the server via query strings in the URL (e.g., `?param=value`).                                                                                                                                                                                                            |
| POST    | Sends data to the server. It can handle multiple input types, such as text, PDFs, and other forms of binary data. This data is appended in the request body and is present after the headers. The POST method is commonly used when sending information (e.g., forms/logins) or uploading data to a website, such as images or documents. |
| HEAD    | Requests the headers that would be returned if a GET request was made to the server. It doesn't return the request body and is usually made to check the response length before downloading resources.                                                                                                                                    |
| PUT     | Creates new resources on the server. Allowing this method without proper controls can lead to uploading malicious resources.                                                                                                                                                                                                              |
| DELETE  | Deletes an existing resource on the webserver. If not properly secured, deleting critical files on the web server can lead to Denial of Service (DoS).                                                                                                                                                                                    |
| OPTIONS | Returns information about the server, such as the methods it accepts.                                                                                                                                                                                                                                                                     |
| PATCH   | Applies partial modifications to the resource at the specified location.                                                                                                                                                                                                                                                                  |

The list only highlights a few of the most commonly used HTTP methods. The availability of a particular method depends on the server and the application configuration. For a full list of HTTP methods, you can visit this [link](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods).

> Note: Most modern web applications mainly rely on the `GET` and `POST` methods. However, any web application that utilizes REST APIs also relies on `PUT` and `DELETE`, which are used to update and delete data on the API endpoint.

### Response Codes

HTTP status codes tell the client the status of their request. An HTTP server can return five types of response codes:

| Type | Description                                                                                                                        |
|------|------------------------------------------------------------------------------------------------------------------------------------|
| 1xx  | Provides information and does not affect the processing of the request.                                                            |
| 2xx  | Returned when a request succeeds.                                                                                                  |
| 3xx  | Returned when the server redirects the client.                                                                                     |
| 4xx  | Signifies improper requests **from the client**. For example, requesting a resource that doesn't exist or requesting a bad format. |
| 5xx  | Returned when there is some problem **with the HTTP server**.                                                                      |

The following are some of the commonly seen examples from each of the above HTTP method types:

| Code                      | Description                                                                                                                                                |
|---------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 200 OK                    | Returned on a successful request; the response body usually contains the requested resource.                                                               |
| 302 Found                 | Redirects the client to another URL. For example, redirecting the user to their dashboard after a successful login.                                        |
| 400 Bad Request           | Returned on encountering malformed requests, such as requests with missing line terminators.                                                               |
| 403 Forbidden             | Signifies that the client doesn't have appropriate access to the resource. It can also be returned when the server detects malicious input from the user.  |
| 404 Not Found             | Returned when the client requests a resource that doesn't exist on the server.                                                                             |
| 500 Internal Server Error | Returned when the server cannot process the request.                                                                                                       |

You can visit this [link](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status) for a complete list of standard HTTP response codes. Besides the standard HTTP codes, servers and providers such as [Cloudflare](https://support.cloudflare.com/hc/en-us/articles/115003014432-HTTP-Status-Codes) or [AWS](https://docs.aws.amazon.com/AmazonSimpleDB/latest/DeveloperGuide/APIError.html) implement custom codes.


#### GET

Whenever we visit any URL, our browsers default to a GET request to obtain the remote resources hosted at that URL. Once the browser receives the initial page, it is requesting, it may send other requests using various HTTP methods. This can be observed through the Network tab in the browser dev tools.

## cURL

[cURL](https://curl.haxx.se/) (client URL) is a command-line tool and library that primarily supports HTTP along with many other protocols. This makes it a good candidate for scripts and automation, making it essential for sending various types of web requests from the command line, which is necessary for many web penetration tests.

![image](https://github.com/user-attachments/assets/4c453681-1840-4fe1-a220-a2ffc20ed44d)

Unlike a web browser, cURL does not render the HTML/JavaScript/CSS code but prints it in its raw format. However, as penetration testers, we are mainly interested in the request and response context, which usually becomes much faster and more convenient than a web browser.

We may also use cURL to download a page or a file and output the content into a file using the -O flag. We want to specify the output file name, we can use the -o flag. Otherwise, we can use `-O` and cURL will use the remote file name as follows:

![image](https://github.com/user-attachments/assets/64eb1344-6740-4a72-9ba7-c136e1557fb0)

In our earlier examples with cURL, we only specified the URL and got the response body in return. However, cURL also allows us to preview the entire HTTP request and the complete HTTP response, which can become very handy when performing web penetration tests or writing exploits. To view the whole HTTP request and response, we can simply add the `-v` verbose flag to our earlier commands, and it should print both the request and response:

```bash
curl inlanefreight.com -v
```

![image](https://github.com/user-attachments/assets/725a3d56-9b01-4535-9d7b-2c774763809a)

![image](https://github.com/user-attachments/assets/593c8967-c79d-40c2-9fe4-cd5ac8fb9b58)

In the previous section, we saw how using the `-v` flag with cURL shows us the full HTTP request and response details. If we were only interested in seeing the response headers, we could use the `-I` flag to send a **HEAD** request and only display the response headers. Furthermore, we can use the `-i` flag to display the headers and the response body (e.g., HTML code). The difference between the two is that `-I` sends a **HEAD** request (as seen in the next section), while `-i` sends any request we specify and prints the headers.

The following command shows an example output of using the `-I` flag:

![image](https://github.com/user-attachments/assets/2cdcdb81-6035-4724-b785-4ba17480dd42)


In addition to viewing headers, cURL also allows us to set request headers with the `-H` flag, as we will see in a later section. Some headers, like the `User-Agent` or `Cookie` headers, have their own flags. For example, we can use the `-A` to set our `User-Agent`, as follows:

![image](https://github.com/user-attachments/assets/0fd49798-712a-4c95-8a1b-b460cb8eafd5)

![image](https://github.com/user-attachments/assets/4df61b27-298a-420f-a311-3f9bda9f7c1c)

![image](https://github.com/user-attachments/assets/c3a4d1a9-2270-4025-a6a6-c8ea1b9fed0b)


#### HTTP Basic Auth

Unlike the usual login forms, which utilize HTTP parameters to validate the user credentials (e.g., POST request), this type of authentication uses a **basic HTTP authentication**, which is handled directly by the webserver to protect a specific page/directory, without directly interacting with the web application.

![image](https://github.com/user-attachments/assets/236b31a3-8e56-4689-a087-582902652e58)

Let's try to access the page with cURL, and we'll add `-i` to view the response headers:

![image](https://github.com/user-attachments/assets/3583f413-7f03-4a71-a1b3-eb7d06126c80)

As we can see, we get **Access denied** in the response body, and we also get `Basic realm="Access denied"` in the `WWW-Authenticate` header, which confirms that this page indeed uses `basic HTTP auth`. To provide the credentials through cURL, we can use the `-u` flag, as follows:

![image](https://github.com/user-attachments/assets/f3b4d193-148c-4d91-8862-2e95bf85aa07)

This time, we do get the page in the response. We can use another method to provide the basic HTTP auth credentials directly through the URL (`username:password@URL`). If we try the same with cURL or our browser, we do get access to the page as well:

![image](https://github.com/user-attachments/assets/eae6aa08-7b80-4edf-9dd1-707a78c8d2ac)

##### HTTP Authorization Header

![image](https://github.com/user-attachments/assets/490eeddf-e733-45f3-ba68-bc8c175049b0)

Using **basic HTTP auth**, we see that our HTTP request sets the `Authorization` header to `Basic YWRtaW46YWRtaW4=`, which is the **base64** encoded value of `admin:admin`. If we were using a modern method of authentication (e.g., JWT), the Authorization would be of type `Bearer` and contain a longer encrypted token.


### cURL for HTTPS

cURL should handle all HTTPS communication standards automatically, perform a secure handshake, and then encrypt and decrypt data automatically. However, if we ever contact a website with an invalid or outdated SSL certificate, cURL, by default, will not proceed with the communication to protect against the earlier mentioned MITM attacks.


