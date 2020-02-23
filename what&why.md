## What is NAT traversal and why should I use it?
NAT traversal provide a method to visit servers behine router or firewall. As we all know, the IPv4 address is limited, the NAT is a way to solve IPv4 address problem, each device behine router use the private address and they use the same public IPv4 address.

### How does it works
The VPN technology is a major method to do NAT traversal

VPN makes computers that running VPN clients can visit each other, for example, there are two clients A, B and a SERVER, they will have three virtual ip address 

SERVER: 192.168.10.1
A: 192.168.10.2
B: 192.168.10.3

A ping B: ping 192.168.10.3

the VPN use layer2 or layer3 forward to make this possible, more about [VPN tunnel](https://github.com/ICKelin/gtun)

so, how to use VPN to do nat traversal, there are two ways.

**1. everyone want to access in the server should run clients, and use virtual IP to visit each other.**
Its safe enough, and every nodes running vpn clients can access the all the nodes in the virtual network. 
The disadvantage is that the vpn client is difficult to develop, you may be need to develop Android,IOS,macOS,windows,linux platforms clients, this may need a big team.

**2. Use VPN server**
we use VPN server as a public server, the SERVER could access all the clients. for example, if you need to access a clients website, you can use nginx's upstream to proxy to A(192.168.10.2)

![](http://www.holenat.net/img/showcase-http.jpg)

```
server {
	listen 80;
	server_name yingjiu.v.holenat.vip;
	location / {
		proxy_redirect off;
		proxy_set_header Host $host;
		proxy_set_header X-Real-IP $remote_addr;
		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
		proxy_pass http://192.168.10.2:8000;
	}
}

```
That will be OK.

The disadvantage is that it may be use by everyone, so you need an authorization for your website.

### Why should I use it
If you are a developer, I think you may use three parts services like facebook, twitter. sometimes we need to receive notification from them, or it calls webhook, which means that once if there are any events, I will call the url you configured in our dashborad. So it also means the service you need to receive the notification must be visit by facebook, so you should deploy the service in public server, NAT traversal service help you to use deploy your service in your local server and export a public url for you.

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

you just need to run you server and listen localhost:9000 and configure http://yingjiu.v.holenat.net/$URI in facebook webhook url.

If you are a geek, may be you like playubg with Raspberry Pi or any other device, but its not share with other, also, you could only play in your home. why not make it public？

If you are a business manager, some employees on business outside office, but some times they need some help or they need some resources in ERP/CMS, VPN may help them with it.

### About IPv6
Since that IPv4 address is limited, the scientist created IPv6 which means ip protocol version 6. So, it is possible that the NAT will be destroyed? I think it depends on the ISP, suggest that everyone can visit your 3389 or 22 port via IPv6 address, I dont think it is safety enough.