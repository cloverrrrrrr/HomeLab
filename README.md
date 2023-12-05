# Intrusion Detection System home lab using Snort

## Description
Building an Intrusion Detection System Home lab, to detect and capture an intrusion in the network using snort with some virtual machine for making the intrusion
<br />

## VM That I used 

- <b>Ubuntu (For snort installed)</b> 
- <b>Kali Linux</b>
- <b>Metasploitable 2</b>

## Operating System

- <b>Windows 10</b> 

## Setting up the Snort

- <b>Install snort in ubuntu machine</b>

  - [How to install snort in ubuntu](https://vitux.com/snort-a-network-intrusion-detection-system-for-ubuntu/)
<br />

- <b>Configuring Snort</b> 

After snort have installed in the ubuntu machine, we have to configure snort for intrusion. in here we have to set an IP address host and the prefix, so the snort know the range of an ip address that we have to detected from an intrusion, before that we have to know the IP network and the prefix by open the terminal and type:
<br />

```bash
  ip a
```
![image](https://github.com/cloverrrrrrr/Snort-home-lab/assets/88470162/f0fb2ee2-bdab-4095-82c8-3e0ed23b28a0)

As you can see in the terminal we have the IP address 192.168.1.10/24, so we can use the IP network from that IP so that is 192.168.1.0/24.

We can continue to configure the IP network so the snort knows what IP should be check to detect the intrude of the network.

```bash
  sudo vim /etc/snort/snort.conf
```

![image](https://github.com/cloverrrrrrr/Snort-home-lab/assets/88470162/546a04b6-a651-4b79-a2f7-7bcfa19f2825)

In here we've to modified the ipvar HOME_NET to our IP network, to modified that just type i to switch in to insert mode, esc for quit the insert mode, and :wq for write and quit the vim. In my case that is ipvar HOME_NET 192.168.1.0/24
Before continue we'll make our vim root user can see the line numbers

```bash
  sudo vim /root/.vimrc
```
and type:

![image](https://github.com/cloverrrrrrr/Snort-home-lab/assets/88470162/99aa8740-4c58-4fbd-9265-d3f88ad0b297)


For additional settings I commented some of the config in snort, because we don't need that. we can back again to snort.conf and type :578,696s/^/# 


![image](https://github.com/cloverrrrrrr/Snort-home-lab/assets/88470162/f141add3-7949-41b3-b020-15b253024ce1)


After that you can quit the vim

<br />



- <b>Making Rules</b> 

Here we're making 2 rules for the detection that is ICMP and SSH, we can put our rules in a file called "local.rules"
    
```bash
  sudo vim /etc/snort/rules/local.rules
```
And type: 

![image](https://github.com/cloverrrrrrr/Snort-home-lab/assets/88470162/08755188-b4a1-4d3e-8553-abef53380c1f)

The first rule, we used icmp on any IP that we've settings before to detect any ping through our network
And the second rule, we set ssh auth attempt on any IP that we've settings before to detect ssh authentication through our network

Now we can test our configuration, using command

```bash
  sudo snort -T -i enp0s3 -c /etc/snort/snort.conf
```

![image](https://github.com/cloverrrrrrr/Snort-home-lab/assets/88470162/6b9ddd1f-ceb2-4ce7-b042-c2328e4dd1ca)

## Detect the Intrusion with Snort

now we're gonna detect our network with snort 

```bash
  sudo snort -q -l /var/log/snort -i enp0s3 -A console -c /etc/snort/snort.conf
```

![image](https://github.com/cloverrrrrrr/Snort-home-lab/assets/88470162/659f094f-8964-4151-953e-c34eda90fff8)

in here we use 
  - -q to quiet operation, because we don't wanna display the banner
  - -l for saving the log
  - -i to select the interface
  - -A for the alert mode
  - -c for which the configuration we want to use

if you want to see the other arguments you can use
```bash
  man snort
```

- <b>Test the intrusion</b>

we're test the intrusion by pinging the ubuntu machine in kali linux 

![image](https://github.com/cloverrrrrrr/Snort-home-lab/assets/88470162/e7de6e8f-9f5d-49f5-9bb2-bce755646854)


and we're gonna see the response from the snort in our ubuntu machine that detect the icmp activity in through our network

![image](https://github.com/cloverrrrrrr/Snort-home-lab/assets/88470162/1bb8ee60-42a8-4b12-b199-0d5870a8a98a)


the second test we're gonna do ssh auth attempt from tcp by activate our Metasploitable 2 and open the kali terminal

![image](https://github.com/cloverrrrrrr/Snort-home-lab/assets/88470162/64ee7445-f6f6-4ead-bc68-b24d67294d9c)


Snort will detect the ssh activity 

![image](https://github.com/cloverrrrrrr/Snort-home-lab/assets/88470162/5503cdca-4b10-4ab2-8300-1d52ea7bcf0e)



<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
