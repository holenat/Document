## Test and debug github webhook
In this case, we will show you how to debug github webhook notification via [hole](http://holenat.net), Its easy to migrate to other webhooks such as facebook.

The finaly operation command should looks like:

```
# step1: run your http server to receive notification
python -m http.server 9000

# step2: run hole to export your http server
hole -auth yDJxBwNvQOeA4pvuK46SGQ== -http 9000

# step3 configuration your webhook...

```

but we give more details step to help you to use hole easier.

- <a href="#download">Download & Install</a>
- <a href="congiguration">Configuration</a>
- <a href="run">Run hole</a>
- <a href="config-github">Receive github webhook message</a>

### <a id="download" href="">Download & Install</a>
Download the hole binary file in out [website](http://holenat.net), we support the following platform

| OS | ARCH | desc |
|---|---|---|
| mac os | amd64 | for mac |
| linux | amd64 | for linux(ubuntu,centos) |
| linux | arm | for respi i386 |
| linux | arm64 | for respi x86_64 |
| windows | x86_64 | for windows x86_64 |

Once downloaded, for mac os or linux, we advice you to move the file to $PATH directory

```chmod +x hole```
```mv hole /usr/local/bin```

### <a href="" id="configuration">Configuration</a>

Before running, we suggest to configure you authtoken first, the authtoken is you unique id. we use authtoken to get your information(username for example)

the hole will save your auth token in hole.conf and will load from hole.conf next time.

**For command line**
```hole -auth $YOUR_AUTH_TOKEN```

for windows user, if you are not good at command line. **double click hole.exe** and fill the authtoken.

```

➜  ~ hole

Welcome for Hole nat service

-----------------------------------------------------
	1、Config AuthToken(OPTION)
	2、Config Local HTTP server port(OPTION)
	3、Config Local HTTP server port(OPTION)
	4、Config Local TCP server ports(OPTION)
-----------------------------------------------------

1、input Authorize Token(REQUIRED):yDJxBwNvQOeA4pvuK46SGQ==
2、input local http port(OPTION):
3、input local https port(OPTION)
4、input local tcp ports(OPTION):

```

close the window after config.




### <a href="" id="run-server">Run http server</a>
Firstly, we need to run a http server to handle github webhook notification. we use python -m SimpleHTTPServer 9000 instead. for python3, you should run python -m http.server 9000

```python2

python -m SimpleHTTPServer 9000

```

```python3

python -m http.server 9000

```

### <a href="" id="run">Run hole</a>
After configure and running http server, its time to run hole to export http://localhost:9000 to public url: http://yingjiu.v.holenat.net

run:

```
➜  ~ hole -http 9000
Hole Nat By ICKelin
status    	 connected
AuthorizeToken	 yDJxBwNvQOeA4pvuK46SGQ==
Username  	 yingjiu
Domain    	 yingjiu.v.holenat.net
Time left 	 2 days 16 hours 7 minutes
Lantancy  	 27ms

Forwarding table:
=============================================================
01. http://yingjiu.v.holenat.net => 127.0.0.1:9000

```


### <a href="" id="config-github">Receive github webhook message</a>
configuration github webhook, for example:


Thas all of the steps