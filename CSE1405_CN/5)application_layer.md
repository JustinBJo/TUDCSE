# Application Layer

---

# Domain Name System
Machines on the Internet are identified by IP addresses, but they are
- hard to remember
- changable

So DNS translates IP addresses into human redable names.

## DNS name space
DNS name space is in a hierarchical structure

![img.png](images/5_images/img.png)

- The top level domains inside the red box are controlled by Internet Corporation for Assigned Names and Numbers (ICANN)
  - .edu and .gov are generic domains usually used by organisations in the US
  - organisations can request second-level domains (like cisco - eng) from registars
  - countries have their own first-level domains (like au, jp, etc)

If you control a domain, you can specify arbitrary subdomains.

## Name servers
To translate a domain name to an IP address, you ask a name server which is configured by DHCP

![img_1.png](images/5_images/img_1.png)

## DNS and transport layer
DNS uses UDP because TCP would be very slow
- Handshake with each of the involved name servers creates a lot over overhead for only one packet
- Leads to security and privacy issues