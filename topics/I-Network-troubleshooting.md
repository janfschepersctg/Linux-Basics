# Network troubleshooting
## introduction 
Due to more and more network access needed in most of the distributed applications today, the restrictions which need to be applied for network access and monitoring has only increased.

## Common networking tools
### ping

The `ping` command, might be one of the most frequently used commands by sysadmins, it uses ICMP packages to check if two machines are connected.

Syntax:

```bash
ping 191.168.1.100
```

You could also `ping` a domain name in order to find out what IP it resolves to:

```bash
ping devdojo.com
```
### traceroute

The `traceroute` command shows you the path from your current machine to your remote server/system and each hope along the way.

Syntax:

```bash
traceroute devdojo.com
```

The output of the above command would look like this:

```bash
 1  164.122.64.253 (164.122.64.253)  1.081 ms  1.064 ms  1.056 ms
 2  168.197.249.56 (168.197.249.56)  1.382 ms 168.197.249.60 (168.197.249.60)  11.573 ms 136.197.249.54 (136.197.249.54)  1.054 ms
 3  168.197.250.149 (168.197.250.149)  0.981 ms 168.197.250.137 (168.197.250.137)  0.995 ms  0.980 ms
 4  de-cix-frankfurt.as13335.net (80.81.194.180)  2.513 ms  2.509 ms  2.501 ms
 5  104.26.11.219 (104.26.11.219)  1.331 ms  1.369 ms  1.359 ms

```

Essentially it is similar to `ping` but it shows you each step from your server to your remote host.

By using `traceroute` you will be able to tell if the connection from one machine to another is failing and where exactly the connection is lost.

### curl

The `curl` command is probably my personal favorite! You can use it to make HTTP requests.

Syntax:

```bash
curl https://devdojo.com
```

There are many useful arguments that you could use, for example, if you add the `-IL` arguments you would get the headers of your domain:

```bash
curl -IL https://devdojo.com
```

### wget

The `wget` command is quite similar to `curl` but has fewer options

I often use it to just download a file:

```bash
wget http://yourdomain.com/some_file.txt
```
### dig

The `dig` command is a great tool for troubleshooting different DNS problems. It is used for DNS lookups, for example, if you wanted to know the A record fo your domain name you would have to run the following command:

``` bash
dig a yourdomain.com
```

And in case you are not receiving emails, the first thing that you would check is if your MX record is correct:

```
dig mx yourdomain.com
```

### whois

The `whois` command is used to get the information related to a domain name.

Syntax:

```
whois devdojo.com
```

As a response, you would get useful information like when the domain was registered, the expiration date, the current nameservers, and the registrar information.

### ifconfig

The `ifconfig` command is used to inspect the current network configuration on your server. It can show you information like:

-   Your IP address
-   Your MAC address
-   All other interfaces attached to your current machine

I'm a big fan of the `ifconfig` command as I really like the output and I'm used to it, but you need to keep in mind that the `ifconfig` command is now deprecated and you should be using the `ip` command instead.

### telnet

Before there was `SSH`, `telnet` was the go-to protocol for connecting from one server to another.

However as `telnet` is insecure, nobody nowadays should use `telnet` for connections.

However, you might still use the `telnet` client to test the connectivity from your local machine to a remote server on a specific port.

For example, if you wanted to check if port `80` on a remote server is open, you could run the following command:

```bash
telnet devdojo.com 80
```
### Netstat/ss

As a system administrator, I use the `netstat` command super often! It shows you the network statistics on your machine, for example, if you wanted to see all of the connections port 80, you could just run the following command:

``` bash
netstat -plant | grep 80
```

You could also use `netstat` to see what services are running and listening on your machine as well.

``` bash
netstat -plant | grep LISTEN
```

As much as I love the `netstat` command it is now being replaced with the `ss` command. It is faster and provides more information.

Syntax:

```bash
ss -lt
```

## Sources
- https://devdojo.com/serverenthusiast/top-15-linux-networking-tools-that-you-should-know
