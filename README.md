# InstallingandConfiguringSnort
# PROJECT NAME

Installing and Configuring Snort 

## Objective

Today I am going to install Snort on my Ubuntu machine. 

### Tools Used

- Snort

## Steps

The first thing I am going to do is update my system by running the following command.

![image](https://github.com/user-attachments/assets/18c6cea5-c680-462e-8db8-d8b0a0bc89d0)

After a few minutes the update is complete. Now I need to install Snort. I run the following command.

![image](https://github.com/user-attachments/assets/a5cb91d5-4b41-4ffb-a445-513497634d16)

Once installation is complete. I am met with the following. I hit okay.

![image](https://github.com/user-attachments/assets/f521f6a8-7148-401e-b2c0-92bdffb2a4d3)

Now I need to put in the IP address of my network adapter here. 

![image](https://github.com/user-attachments/assets/170707e0-7754-4c58-8a38-7ba021ba5d3b)

I open up a new terminal and run the command ip addr highlighted is what I am looking for. 

![image](https://github.com/user-attachments/assets/1ee6a7f3-2f7f-4c48-b873-a80336e20b9d)

I only need the first part of the IP address to cover the range of 256 addresses and its a /24 network. I enter 192.168.1.0/24

The install is complete. Since my NIC (Network Interface Card) is configured to only receive the packets meant for them as the destination, I won’t be seeing the other packets coming in. That means I now need to put my NIC  into promiscuous mode. 

I run the following command. From the previous step I know my  NIC is enp0s3

![image](https://github.com/user-attachments/assets/18f69311-aee0-4634-86b2-22b561f05355)

It asks for my password. Once that is complete I open a new window to see if it worked. I run the command ip addr. I can see that PROMISC is on.

![image](https://github.com/user-attachments/assets/1e3eb58d-17ee-47d9-8bb8-028007509a56)

Now that this is complete. I will go into the configuration file and make some changes. Some people use vim, I am just going to keep it simple and use nano. 

![image](https://github.com/user-attachments/assets/4eb54f49-0f0c-43a4-b2b3-dd0e6cd84e0f)

I scroll down to HOME_NET and put in the same IP address as I had. CTRL X, Y to Save and save the config file. 

![image](https://github.com/user-attachments/assets/884fd1b7-3acd-4646-8ba6-06ed83cd210d)

Now that I have successfully installed and configured Snort. I am going to set some rules. There are 4 categories of Snort rules: Community Rules, Registered Rules, Subscription Rules, and Build Your Own Rules.

I will be editing the local rules file using nano- sudo nano /etc/snort/rules/local.rules

I will be setting a very simple rule to prompt alert if a ping is received on my home network. I will be opening my Kali Linux machine later to test if the rule is working. 

![image](https://github.com/user-attachments/assets/988461ca-7295-4e8b-8ea2-dc6abc461341)

Rule breakdown from left to right:  

- alert is the type of action that will be taken. I just want to be alerted.
- icmp is the protocol
- any any is from any source IP and port
- - (>) is the direction of the traffic.
- $HOME_NET will be my home network.
- any would be the destination port.
-  msg would be the message the alert would generate in the logs.
- sid is the Snort ID and rev is revision #

Now that I have added a custom rule. I save the rule file. 

I will now run Snort in quiet mode with the below command. 

![image](https://github.com/user-attachments/assets/eefe906d-06aa-4335-8baa-2fb432d4d377)

If nothing happens it means its working. I open up my Kali Linux machine to test this out. 

![image](https://github.com/user-attachments/assets/8edca13f-ac14-4cac-9efc-3be60ef09e9f)

It works. I can see here alerts being generated.

![image](https://github.com/user-attachments/assets/c0ce128d-a343-4848-8478-f5b57c591601)

Now I will check the log file with the following command.

![image](https://github.com/user-attachments/assets/d3b58dba-742e-4f57-9ad9-911ded9d2352)

Looks like I got 48 packets. None were dropped as I only set up a rule to trigger alerts. 

![image](https://github.com/user-attachments/assets/2cd7112c-aa2a-4da2-90c4-ec5542ebadc3)

Here we can see the actual alerts, the source and destination IP.

![image](https://github.com/user-attachments/assets/59de422e-35db-4d8d-b6e7-824908527f27)

Perfect. Snort is a great IDS/IPS with plenty of community support. There are a ton of documentations and YouTube videos that will assist with confuguration and rule building. 

End
