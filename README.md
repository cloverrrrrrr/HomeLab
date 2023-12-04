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

In here we've to modified the ipvar HOME_NET to our IP network, to modified that just type :i to switch in to insert mode, esc for quit the insert mode, and :wq for write and quit the vim. In my case that is ipvar HOME_NET 192.168.1.0/24
Before continue we'll make our vim root user can see the line numbers

```bash
  sudo vim /root/.vimrc
```
and type:

![image](https://github.com/cloverrrrrrr/Snort-home-lab/assets/88470162/99aa8740-4c58-4fbd-9265-d3f88ad0b297)


For additional settings I commented some of the config in snort, because we don't need that. we can back again to snort.conf and type :632,750s/^/# 


![image](https://github.com/cloverrrrrrr/Snort-home-lab/assets/88470162/3e8368cc-36e0-4543-905a-371003dac250)

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



<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
