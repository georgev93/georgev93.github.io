---
---

# Domain Name System (DNS)

(Quick note, the primer on IP addresses may be helpful before you read this primer)

Domain Name System is what translates URLs into ip addresses. It is the "Phone Book" of the internet. For example, let's look at what happens when I type `https://google.com` into my browser:

 1. Because I typed in a "https" address into my browser (modern browsers will add `https://` if you leave it off), it knows it's going to ask port 443 of a server for a webpage. It doesn't know where this server is right now, it just knows it's at the URL `google.com`. It needs to resolve this URL into an IP address.
 2. It checks the cache of URL/IP address combinations on the local computer. Let's say it doesn't find any record of `google.com`. Now it needs to ask someone for the address.
 3. My computer has to ask a DNS server for the record. The DNS server my computer reaches out to is either the one I set or the one that my router suggested when I connected to the wifi (this DNS suggestion happened during the "DHCP" process when my device connected). Let's say the DNS my computer is going to reach out to (either because I set the setting on my computer or this is the DNS server the router suggested) is `1.1.1.1`. My computer sends a "DNS Request" containing the question "What is the IP of `google.com`?" to port 53 (the DNS port) of `1.1.1.1`.
 4. The DNS server responds with a "DNS response" containing the response "`google.com` is at `172.253.122.102`".
 5. My computer can now continue with the original request. It requests a webpage from port 443 (the https port) of `172.253.122.102`.
 6. `172.253.122.102` sends my computer a webpage. My browser displays that webpage.
 7. I interact with the webpage, typing in "pictures of ducks" into the search bar. When I click "Google Search", the webpage tells my computer it should request a webpage from `https://google.com?q=pictures+of+ducks`. So it builds up an https request for content with the label `?q=pictures+of+ducks` from `google.com` (port 443). We need to know the address of `google.com` again...
 8. My computer checks its local cache for any entries that match `google.com`. Success! It found a cached record of a DNS exchange requesting the address of `google.com`. It's recorded that it's at `172.253.122.102`. I don't need to talk to the DNS server again right now (because that would take some time).
 9. My computer sends that `?q=pictures+of+ducks` https request to `172.253.122.102` at port 443.
 10. Google sends a webpage with pictures of ducks. My browser displays it.

So you can see, when you access a website, you sometimes (but not always!) need to start with a "DNS Request" to find the address of the URL.

## mDNS

If you use a url ending in any of the following: `.local`, `.localdomain`, or `.lan`, your device recognizes that you're not trying to reach the internet, it is instead trying to talk to someone on the same network. Instead of sending a DNS request to the DNS server, it broadcasts a message to everyone on the network trying to find out who has that address. For instance, if I type `nas.local` into my computer, it broadcasts a message to the local network asking "Who has `nas.local`?". If a device on my network listens to that address, it will respond "That's me! Contact me at `192.168.1.2`."

Listening for mDNS broadcasts requires software to be running on the computer so it can be ready to respond. On Windows machines, it's called "Bonjour". On Linux, it's "Avahi". It's usually running by default, and will respond to URLs that are the "hostname" of that device `.local`. If you set up your nas to have the hostname "mysupercoolnas", it will respond when a device broadcasts that it's looking for `mysupercoolnas.local`, `mysupercoolnas.localdomain`, or `mysupercoolnas.lan`.

## DNS Rebinding

If you run your own DNS server, you set up your router to configure devices on the network to use that server's IP address as the primary DNS server. That means your DNS server can respond back with its own address book. If the requested url isn't in its address book, you could forward it on to another DNS server (like a legitimate one on the internet).

Why do this? This is how people "ad block" on their network. Say you want to go to `cnn.com`. You go to the website, and the website tries to load an add on the side of the page that has the url `banner.ads.com`. If your device is going to your local DNS server with all of its requests, you could have an entry in your address book that correlates `banner.ads.com` to address `0.0.0.0`... nowhere... unreachable. `cnn.com` on the other hand isn't in your local address book, so your DNS server knows to forward those DNS requests to the real internet and get a real response. The result: The page loads, but all of the ads fail to load! Thanks to open source services like "PiHole", people keep a very up to date blacklist of urls associated with ads/trackers as well as a whitelist of sneaky urls the website makes sure you can load before letting you see the page (traps to detect ad blockers). So you can set up your own DNS server on your network, tell it to get the most up-to-date lists from websites that maintain these whitelists and blacklists, and then you have no ads on your home network across all of your devices!

In addition, let's say you want to access devices on your network with `nas.myhome.com`. Without your own DNS server, you'll get a DNS response giving you an address to some `myhome.com` website on the internet. If you have your own DNS server, it has first dibs at responding, so it can tell devices on your network that `nas.myhome.com` is `192.168.1.2`. Boom. You have a customizable local domain name now!
