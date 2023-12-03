# Intrusion Detection System home lab using Snort

## Description
Building an Intrusion Detection System Home lab, to detect and capture an intrusion in the network using snort with some virtual machine for making the intrusion (TCP and ssh)
<br />

## VM That I used 

- <b>Ubuntu (For snort installed)</b> 
- <b>Kali Linux</b>
- <b>Metasploitable 2</b>

## Operating System

- <b>Windows 10</b> 

## Program walk-through:

- <b>Install snort in ubuntu machine</b>

  - [How to install snort in ubuntu](https://vitux.com/snort-a-network-intrusion-detection-system-for-ubuntu/)
<br />

- <b>Configuring snort for detection</b> 

  - After snort have installed in the ubuntu machine, we have to configure snort for intrusion. in here we have to set an IP address host and the prefix, so the snort know the range of an ip address that we have to detected from an intrusion, before that we have to know the IP network and the prefix by open your terminal and type:
<br />

```bash
  ip a
```


<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
