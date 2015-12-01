## Port forwarding 80 to 8080 on Mac OSx Yosemite.

Create a bin directory under your home folder, step # 1,2,3 is necessary if you want to access and run the script from anywhere you want

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
