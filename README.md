**Download link of the vulnerable machine Dripping_Blue**
https://download.vulnhub.com/drippingblues/drippingblues.ova


# Dripping_Blue
In this repository I will be explaining the solution of the Dripping_Blue1 laboratory where I will give you the step by step, how to do it and if you have any questions, do not hesitate to contact us.

PASSIVE RECOGNITION.

1. There is a login to the machine in which a password is requested, which is the objective of this laboratory, in order to enter it.
   
![image](https://github.com/moistealth/Dripping_Blue/assets/108200081/ce3b183f-7608-4dff-b444-94462d9bf73c)

2. From the attacking machine execute the *netdiscover* command to review our network and thus be able to identify the IP of the target machine.
   
![image](https://github.com/moistealth/Dripping_Blue/assets/108200081/6adc9dae-42a8-468f-8c5d-10154dbc56c0)

3. Later we ping the target machine to verify connection.

![image](https://github.com/moistealth/Dripping_Blue/assets/108200081/8609c3ed-302e-42f0-b226-bdcd4270a24f)

4.Perform a scan with nmap for enumeration and detection of services.
*nmap -sC -sV <IP>*


5. ports are identified
*(21,22,80)*
and it is possible to identify something important and that is that you have an anonymous connection via ftp and you can see a zip file with the name
*(respectmydrip.zip)* , here we already have something that we will see later.

![image](https://github.com/moistealth/Dripping_Blue/assets/108200081/effb467f-cbda-4250-8afc-dad4a68a1401)

6. Then we'll do a reconnaissance on port 80 to see what we can get.
With the following command we will make an http request to see what we get.
*curl http://IP*

![image](https://github.com/moistealth/Dripping_Blue/assets/108200081/deeaeecb-b87a-494c-bb41-243d05a3ec70)
*a message was obtained that does not help much, a small stumble*

**WE WILL MAKE A DISCOVERY OF POSSIBLE DIRECTORIES TO EXPAND OUR SCENARIOS (I will explain two ways to make this listing)**


7.The first way is by using the *dirb <ip>* command which uses a default dictionary to list directories.
We get the following:

![image](https://github.com/moistealth/Dripping_Blue/assets/108200081/ad97af3e-04ff-46ce-bc2b-1585daf3baae)

8. The next way to do it is using *gobuster* with the following command it performs the same procedure as *dir* but this time in a more organized way.
*gobuster dir -u http://<IP> -x html,txt,php,bak --wordlist=/usr/share/wordlists/dirb/common.txt*

![image](https://github.com/moistealth/Dripping_Blue/assets/108200081/e5824552-0236-4835-9c82-c38efb98bf03)
*in the image we obtain evidence that we obtain the same results obtained with the previous form, in conclusion we can use one of these two ways to make a list of directories*

9. 
Now we will see what information we can obtain from the directories:
*robots.txt*
*index.php*

![image](https://github.com/moistealth/Dripping_Blue/assets/108200081/2252c5d4-b4e3-4704-8e45-12be062b69e7)
*in our first check to *index.php* we didn't get much*

![image](https://github.com/moistealth/Dripping_Blue/assets/108200081/f5c3e48e-1b22-418f-bc7a-f7dd8b73aea3)
 
 *When reviewing *robots.txt* we see that we get two files that seem to be important, to keep them in focus*


 Well, in this process of passive recognition and enumeration we obtained some information that could be of use to us:
 
- Anonymous connections to ftp and we see a *zip* file
-We identified two apparently important files in the path *robots.txt*


10.Following these we will connect by ftp anonymously with the following credentials *anonymous:anonymous* using the command *ftp <IP>*

![image](https://github.com/moistealth/Dripping_Blue/assets/108200081/f1feca26-e924-405b-b701-2b3cf787df32)

inside we can execute certain commands, in this case we will execute *ls* to list possible files or folders
![image](https://github.com/moistealth/Dripping_Blue/assets/108200081/288f1bcd-d3df-43f6-b592-6710468a29b5)
*We managed to identify the file listed above in the passive acknowledgment*

*Then we proceed to export that zip file in our local directory with the command *get <file name>*

![image](https://github.com/moistealth/Dripping_Blue/assets/108200081/440c3712-3593-4715-a633-fdc6f7c8f793)


*With the *unzip* command we try to unzip the file, but we are surprised that it has a password :O*
![image](https://github.com/moistealth/Dripping_Blue/assets/108200081/0050d0a5-d89e-4c5b-83ff-a01373cec124)


But when we press enter, leaving the password empty, we see that a compressed file *secret.zip* is extracted, this means that only the *txt* file was the one that required a password
![image](https://github.com/moistealth/Dripping_Blue/assets/108200081/ea386731-1638-4c07-83dd-1d6006009302)
![image](https://github.com/moistealth/Dripping_Blue/assets/108200081/d2476a54-1405-40e4-8219-89df801a3af3)


we use fcrackzip to do a brute force attack to discover the password of the *zip* file and in this way extract the *txt* file, we use the following command: *fcrackzip -D -p /usr/share/wordlists/rockyou.txt -u respectmydrip.zip*

![image](https://github.com/moistealth/Dripping_Blue/assets/108200081/9e4e3991-32f4-40d1-a806-629bbe76819d)
*we obtain the password of the zip file which is: *072528035**


![image](https://github.com/moistealth/Dripping_Blue/assets/108200081/408ca3e2-bb40-4445-8fdd-c6f18a5010af)
*we unzip the file and put the password and eureca we get the txt file*


when opening the file it tells us to focus on drip
![image](https://github.com/moistealth/Dripping_Blue/assets/108200081/e3d5def5-19c4-4cdb-939a-794687297b1f)


later we will review the path of robots.txt to see what we can do from there

![image](https://github.com/moistealth/Dripping_Blue/assets/108200081/f6d1e7c0-dd42-481a-ac4d-08a108d3ea80)


when accessing the second route we have an LFI which allows us to access and read system files by manipulating routes in requests

![image](https://github.com/moistealth/Dripping_Blue/assets/108200081/6253fc18-1112-4539-bfb6-d66b82fb2d18)
![image](https://github.com/moistealth/Dripping_Blue/assets/108200081/8c2cca22-c41b-491a-b2b3-f5eb633c8fad)


By having a remote code execution we can read files, we will go to the path */etc/passwd*
![image](https://github.com/moistealth/Dripping_Blue/assets/108200081/65fa6435-1335-4ec9-a515-ec8222adcd5f)
*This information was obtained, now we will look for a valid user*


we found the user of the victim machine
![image](https://github.com/moistealth/Dripping_Blue/assets/108200081/c3576fcf-dd45-4c50-a3e4-2c94b6b9f10d)


**Now we will try that password on the target machine to verify if it is the password of that user**


WE VALIDATE AND READY WE ARE INSIDE, NOW TO LOOK FOR THE FLAG
![image](https://github.com/moistealth/Dripping_Blue/assets/108200081/224fd67b-610a-4d25-a5f7-c29c2167cd9e)



