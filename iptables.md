# Iptables

1. Filter Table -> will filter incoming and outgoing traffic
2. NAT Table -> is used to redirect connections to other interfaces
3. Mangle Table -> is used to modify packets or connections

- Filter Table

  1. Input Chain
  2. Output Chain
  3. Forward Chain

- NAT Table

  1. Output Chain
  2. Pre-Routing Chain
  3. Post-Routing Chain

- Mangle Table
  1. Input Chain
  2. Output Chain
  3. Forward Chain
  4. Pre-Routing Chain
  5. Post-Routing Chain

## Filter Table

This is the part of iptables which is responsible for incoming and outgoing traffic, so this is the part of the iptables which is used as firewall. To handle traffic firewall rules are set to block or allow traffic. If we have a firewall rule set to block all the ftp traffic, it will block a ftp request and when it matches, a target will be set.
**Target** are something which will define what is going to happen to a particular packet when it is blocked.
There are 3 ways we can handle a target

1. Accept -> will allow the packet to process
2. Reject -> will drop the packet and send a feedback to the user
3. Drop -> will simply drop the packet without caring to give any feedback

### Commands to handle firewall

Before setting up firewall make sure to flush iptables which can be done with **`sudo iptables -F -v`**. -v is just for verbose output and it doesn't have any effect on function of the flush.

- **List all the tables** => `sudo iptables -L`
- **Default Policy for different chains** => when we list all tables it will also have a default policy set and represented in parenthesis as (policy ACCEPT) which means a particular chain will accept any packets.
- **Setting default policy for chains** => `iptables --policy INPUT DROP` This will drop all the incoming packets to the server. CAUTION: REJECT can't be set as default policy as it is a target extension and only work on targets.
- **Block an IP Address to connect to server** => `iptables -I INPUT -s 321.43.234.24 -j REJECT` This specify that if there is an incoming packet from a particular ip address reject it.
  We can add the rule on the top of the list or bottom of the list. To add the rule to the top we use `-I` and to add it to the bottom of the list we use `-A`.
  We specify the IP Address using source flag `-s`. It can also have subnet like 1.23.23.124/932 where 932 is subnet
  Target is specified using `-j` and will have value of ACCEPT REJECT DROP.

### Delete a Rule

To delete a rule we need to get the line number of the rule which can get by running `iptables -L --line-numbers`. After getting the line numbers we can use `-D` flag to delete a rule at particular line number using `iptables -D INPUT 1` where `-D` flag is used to delete a particular rule and INPUT specify that we are deleting rule from INPUT chain and 1 is the line number of that rule.

### Blocking a connection on a particular protocol and port

We can block a particular protocol to connect with server using iptables. If we are creating a http server it will make sense to allow connections on only port 80 with tcp protocol.
To specify the protocol we use `-p` flag. `--dport` flag can be used to set the destination port which will specify the port number. This will look like this `iptables -I INPUT -p tcp --dport 80 -s 192.168.1.11 -j ACCEPT`

**We need to save the rules to make them persistent** which can be done with `sudo /sbin/iptables-save`.

## NAT Tables

NAT Tables are used to redirect or forward the connection.
