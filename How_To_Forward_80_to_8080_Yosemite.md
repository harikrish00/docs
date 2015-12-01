## Port forwarding 80 to 8080 on Mac OSx Yosemite.
Purpose:
Why do you want to forward 80 to 8080?
Typical use case is, when you do a local web development you want to test your changes progressively. And you would do this a million times a day by launching the url on the browser like this http://localhost:8080
Two things, 1. you have to enter the port everytime and 2. it looks ugly. When you launch any url in the browser without a port at the end, browser assumes port 80 by default. 

- For example
```www.google.com``` is translated as ```www.google.com:80```

So start your local application in port 8080 if it doesnt do by default, for example all rails projects start your app on default port 3000. In that case do the following

``` rails s -p 8080 ```

follow along my document here, and once you  have successfully created the script and did the port forwarding you can access your app without any port now.


Create a bin directory under your home folder, this will let you run the script globally

- cd ~
- mkdir bin
- cd bin
- vim fwd80.sh
- press I

and paste this below code into it

```
echo "
rdr pass inet proto tcp from any to any port 80 -> 127.0.0.1 port 8080
" | sudo pfctl -ef -
```

- presee ESC + :wq + Hit Enter
- chmod +x fwd80.sh
- vim ~/.bash_profile

add the below line on the top of the file, DONT FORGET TO REPLACE YOUR USER ID

```
export PATH=/Users/<your user id>/bin:$PATH

```

- source ~/.bash_profile
- quit the terminal and relaunch it

Run the below command to do make it effective

- fwd80.sh

Sample result will look like below
```
pfctl: Use of -f option, could result in flushing of rules
present in the main ruleset added by the system at startup.
See /etc/pf.conf for further details.

No ALTQ support in kernel
ALTQ related functions disabled
pfctl: pf already enabled
```
