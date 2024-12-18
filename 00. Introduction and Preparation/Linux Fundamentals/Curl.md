# CURL

[Curl](https://www.kali.org/tools/curl/) is a command-line tool for transferring data with URL syntax. It supports DICT, FILE, FTP, FTPS, GOPHER, HTTP, HTTPS, IMAP, IMAPS, LDAP, LDAPS, POP3, POP3S, RTMP, RTSP, SCP, SFTP, SMTP, SMTPS, TELNET, and TFTP.

Curl supports SSL certificates, HTTP POST, HTTP PUT, FTP uploading, HTTP form-based upload, proxies, cookies, user+password authentication (Basic, Digest, NTLM, Negotiate, Kerberos…), file transfer resume, proxy tunneling, and a busload of other useful tricks.

## HyperText Transfer Protocol (HTTP)

Today, the majority of our applications, both web and mobile, constantly interact with the Internet. Most Internet communications are made with web requests through the HTTP protocol. HTTP is an application-level protocol used to access World Wide Web resources. The term hypertext stands for text containing links to other resources and text that readers can easily interpret.

HTTP communication consists of a client and a server, where the client requests the server for a resource. The server processes the requests and returns the requested resource. The default port for HTTP communication is port 80, which can be changed to any other port, depending on the web server configuration. The exact requests are utilized when visiting different websites on the internet. To reach the desired website, we enter a Fully Qualified Domain Name (FQDN) as a Uniform Resource Locator (URL).

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
| Method  | GET               | The HTTP method or verb, which specifies the type of action to perform.                                             |
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


### cURL for HTTPS

cURL should handle all HTTPS communication standards automatically, perform a secure handshake, and then encrypt and decrypt data automatically. However, if we ever contact a website with an invalid or outdated SSL certificate, cURL, by default, will not proceed with the communication to protect against the earlier mentioned MITM attacks.


