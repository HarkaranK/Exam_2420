# Exam_2420

<h1>Author: Harkaran Kang</h1>

<h2>Part 1</h2>

To update most of the software on your Ubuntu OS

1) Run the following command
```
sudo apt-get-update
```

2) Now that everything that should be updating is stated, run the following command
```
sudo apt-get upgrade
```


<h2>Part 2</h2>

1) Fixing the following code

```
if [ $# -eq 1 ] ; then
  eco "Usage: $0 temperature[F|V|K]
        where the suffix:
        F    indicates input is in Fahrenheit (default)
        V    indicates input is in Celsius
        K    indicates input is in Kelvin"
   exit 1
fi

unit="$(eco $1|sed -e 's/[-[numbs]]*//g' | tr '[:lower:]' '[:upper:]' )"
temp="$(eco $1|sed -e 's/[^-[:digit:]]*//g')"
```

2) First open the code up with vim
```
vim <filename>
```

3) Enter ```i``` to go into **insert mode** then paste the code

4) Then change the code to look like the screenshot below (Use arrow keys to move around in Vim)

5) The code should look something like this

Part2_HowCodeShouldLook.png

6) Once your done editing press ```esc``` then type ```:wq!```
7) That will save and exit


<h2>Part 3</h2>

1) Open the journalctl man by typing ```man journalctl```
2) Search for boot with ```/boot``` and look for the same part as the screen shot below

Part3_ManBoot.png

3) Next search for Warnings with ```/warning``` and look for the same part as the screen shot below

Part3_ManWarning.png

4) Search for Json with ```/json``` and look for the same part as the sreen shot below

Part3_ManJson.png

5) Now that all the neccessary information that is needed is found, exit vim by pressing ```enter``` then press ```q``` afterwards

6) Create a file where we will write our command, enter ```logger -t -f /var/<filename>.log
7) Now open the fill up with 



<h2>Part 4</h2>

1) Enter the command ```sudo adduser <username>```
2) Follow the steps and when prompted for the full name press ```Ctrl C```
3) To test if it worked enter ```ls /home``` if done correctly you should see your new user
4) Do steps 1-3 one more time

Part4_TestUsers.png

Now that we have 2 test users we can continue

5) Create a bash script by typing ```vim <filename>```
6) Copy the code below

```
#!/bin/bash

echo "Regular Users (UID 1000-5000)"
echo
grep -E ":([1][0-9][0-9][0-9]|[2-4][0-9][0-9][0-9]|[5][0-9][0-9][0-9]):" /etc/passwd | awk -F : '{print $1"\t"$3"\t"$7}'

echo
echo "Currently Logged In Users"
echo
who | awk '{print $1}'
```

Part4_FindUsers.png

7) chmod +x <filename> 
8) Change the code now to

```
#!/bin/bash

echo "Running command"

echo "Regular Users (UID 1000-5000)" > /etc/motd
echo >> /etc/motd
grep -E ":([1][0-9][0-9][0-9]|[2-4][0-9][0-9][0-9]|[5][0-9][0-9][0-9]):" /etc/passwd | awk -F : '{print $1"\t"$3"\t"$7}' >> /etc/motd

echo >> /etc/motd
echo "Currently Logged In Users" >> /etc/motd
echo >> /etc/motd
who | awk '{print $1}' >> /etc/motd
```


9) To run the command type ```sudo ./<filename>```


<h2>Part 5</h2>

1) To start editing your service file run the following command

```
sudo vim /etc/systemd/system/<service file name>.service
```

Make sure to change the file path in **Service to your own**

```
[Unit]
Description=Will run the ./find_users command

[Service]
Type=simple
ExecStart=/usr/bin/bash ~/exam/find_users

[Install]
WantedBy=multi-user.target
```




Part5_ServiceFileContents.png

2) Run the following commands

```
systemctl reload daemon
systemctl enable <service file name>
systemctl start <service file name>
systemctl status <service file name>
```


