# CURL

[Curl](https://www.kali.org/tools/curl/) is a command-line tool for transferring data with URL syntax. It supports DICT, FILE, FTP, FTPS, GOPHER, HTTP, HTTPS, IMAP, IMAPS, LDAP, LDAPS, POP3, POP3S, RTMP, RTSP, SCP, SFTP, SMTP, SMTPS, TELNET, and TFTP.

Curl supports SSL certificates, HTTP POST, HTTP PUT, FTP uploading, HTTP form-based upload, proxies, cookies, user+password authentication (Basic, Digest, NTLM, Negotiate, Kerberos…), file transfer resume, proxy tunneling, and a busload of other useful tricks.

## HyperText Transfer Protocol (HTTP)

Today, the majority of our applications, both web and mobile, constantly interact with the Internet. Most Internet communications are made with web requests through the HTTP protocol. HTTP is an application-level protocol used to access World Wide Web resources. The term hypertext stands for text containing links to other resources and text that readers can easily interpret.

HTTP communication consists of a client and a server, where the client requests the server for a resource. The server processes the requests and returns the requested resource. The default port for HTTP communication is port 80, which can be changed to any other port, depending on the web server configuration. The exact requests are utilized when visiting different websites on the internet. To reach the desired website, we enter a Fully Qualified Domain Name (FQDN) as a Uniform Resource Locator (URL).

### URL

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

### HTTP Flow

![image](https://github.com/user-attachments/assets/dbfe3bf7-55f6-4c8d-aae5-e55efb02d3e5)

The diagram above presents the anatomy of an HTTP request at a very high level. The first time a user enters the URL (inlanefreight.com) into the browser, it requests a DNS (Domain Name Resolution) server to resolve the domain and get its IP. The DNS server looks up the IP address for inlanefreight.com and returns it. All domain names must be resolved this way, as a server can't communicate without an IP address.

> **Note**: Our browsers usually first look up records in the local '/etc/hosts' file, and if the requested domain does not exist within it, they will contact other DNS servers. We can use the '/etc/hosts' to manually add records for DNS resolution by adding the IP followed by the domain name.




