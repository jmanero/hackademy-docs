Boostrapping
============

## Windoze Only: Install Putty
 1. Download

http://the.earth.li/~sgtatham/putty/latest/x86/putty.zip

 1. Unzip
 1. Run putty.exe

## Download the bootstrap SSH key
 * Putty: http://jmanero.m.dyn.io:8081/pub/start.ppk
 * SSH: http://jmanero.m.dyn.io:8081/pub/start.pem

## Login (SSH)

    ssh -i /path/to/start.pem ubuntu@start.m.dyn.io

## Create an SSH key-pair

 1. Create the key-pair: ```ec2-create-keypair --hide-tags {YOUR NAME} > $HOME/.ssh/id_rsa```
 2. Copy/Paste the output into a file **on your laptop**
 3. Change the permissions to 600: ```chmod 600 start.pem```

## Create your "workstation"

    knife ec2 server create -I ami-1d1e7774 -f t1.micro -S {YOUR NAME}

Output:
```text
[DEPRECATION] Defaulting to json library for json parsing. Please consider using multi_json library for the greatest performance/flexibility.
Instance ID: i-1d811e7f
Flavor: t1.micro
Image: ami-1d1e7774
Region: us-east-1
Availability Zone: us-east-1d
Security Groups: default
Tags: {"Name"=>"i-1d811e7f"}
SSH Key: jmanero

Waiting for instance...............................
Public DNS Name: ec2-54-234-143-113.compute-1.amazonaws.com
Public IP Address: 54.234.143.113
Private DNS Name: ip-10-245-75-135.ec2.internal
Private IP Address: 10.245.75.135

Waiting for sshd.........done
Bootstrapping Chef on ec2-54-234-143-113.compute-1.amazonaws.com
ERROR: Errno::ENOENT: No such file or directory - /etc/chef/validation.pem
```

## Log into your "workstation"
**First, log out of start.m.dyn.io:** `exit`

    ssh -i /path/to/{YOUR NAME}.pem ubuntu@{Public DNS Name}
    
Use the key you saved above, and the FQDN displayed in the `knife ec2` output to log into your new worksataion
