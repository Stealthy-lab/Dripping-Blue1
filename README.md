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

