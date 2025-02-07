**# Nmap Introduction**

 Nmap is a network scanning tool that can be used to ascertain what hosts are up on a network or what services are avaiailble among other things
 
**NOTE** I am using a ParrotOS VM running on my windows 11 laptop so results may vary slightly is you use a different OS or even a different linux based OS like kali or ubuntu but the main principles apply

First off its always really good practice to ensure we are on the latest version of linux when first starting just to be safe and it only takes a couple of seconds
```bash
sudo apt update
```
This will quickly update you to the latest version of linux 

then lets quickly make sure that nmap is installed and up to date this can be done with the following 
```bash
sudo apt install nmap
```
Note: if you already have nmap installed this will update to the latest version:)

Next up lets make ourselves a super user! (su) this will allow us to use more nmap syntax than if we were just a normal user
```bash
sudo su
```
simple right? depending on your OS and setup of your machine it might require a password **NOTE** linux will not show your password as you type so dont worry just type the password and press enter if you get it wrong. Dont do what I did and troubleshoot a broken keyboard for 20 minutes.

Last bit of prep is just to test we are actually able to send messages to the IP and get messages back, Thankfully there is a nifty command we can use to quickly and easily find out
```bash
ping <target IP>
```
this tells you lots of useful information like the size of the packets being sent, the time it takes for packets to go to the IP and back. and even the time to live (TTL) which if you know your stuff can help you figure out what OS the other network is using


**#using the Nmap command**

Use the `nmap` command to scan the network.

```bash
nmap <target IP>
```

simple right? this should hopefully let us know what ports are availible and how many hosts are up

```bash
nmap -sV <target IP>
```

This will perform a relatively basic scan that also tells us the service version helpful for making sure we are up to date or if our target is running behind on their updates leaving them vulnerable

When I test this on my IP i usually return an error as this is a very basic scan and is often blocked. The handy thing about parrot though is that it can sometimes suggest alternative syntax you can use to try and get around it
```bash
#in this instance the following change in syntax suggested by parrot worked a charm
nmap -Pn <target IP>
```
This reveals what ports are open and how many hosts return a signal which can helps us determine what ports are vulnerable or what we can use for a penetration test or something of that nature

lets say we are getting an error and we know the host is up but either there are 0 open ports or our nmap is returning with nothing we can try a "sneaky scan" or a "synscan" (thats the actual name) this will allow us to bypass any kind of basic restriction on an nmap scan lets try it

```bash
nmap -sS <target IP>
```

Next up lets try a more aggressive scan. Literally this next nmap syntax is -A and is known as an aggresive scan

```bash
nmap -A <target IP>
```
This will take a bit more time but will find out alot more information if it goes through 

information relating to what internet of things(IOT) device is responsible for what port is open. 

Sometimes you might still be unable to get an nmap to return any details. This can be due to intrusion Detection System(IDS) or a firewall. But don't worry we have a work around Decoy Ip addresses!

Heres the syntax
```bash
nmap -D <Decoy IP address> <target IP>
```

this will run a decoy to make it harder for any firewall or IDS to determine your actual IP and prevent access 

to build on that we can use multiple decoys at once to make it even harder to be deteceted however this will increase scan time

```bash

nmap -D <decoy IP1>,<DecoyIP2> <Target IP>
```

To wrap this small demonstration of what you can do with nmap lets end with the "-d" syntax this stands for debug and basically makes nmap tell you whats happening at each step. It's great for trying to learn what nmap is actually doing but it also helps with figuring out what exactly is going wrong if you arent able to get a response

```bash
nmap -d <target IP>
```

This can be combined with other syntax to gain a deeper understanding heres an example:

```bash
nmap -d -A <target IP>
```
this will make the terminal display what exactly doing at each step of the aggresive scan handy right?

And there you have it thank you so much for reading and I hope this has demonstrated a good chunk of the basic nmap features I know in a easily readable manner thanks again!


