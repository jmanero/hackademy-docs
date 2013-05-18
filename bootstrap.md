Boostrapping
============
## Download Private Keys
Use this key to log into EC2 instances that you create. Everyone has a username comprised of
their first initial and last name. e.g John Manero's user name is `jmanero`.
 * Substitute your username: http://jmanero.m.dyn.io:8081/pub/USERNAME
 * The file has no extension (e.g .ppk or .pem)

## Using SSH
Set the correct permissions for the key you downloaded. Substitute your username.

```chmod 600 USERNAME```

Use the `ssh` command to log in to remote servers.

```ssh -i path/to/key USERNAME@HOSTNAME.m.dyn.io```

`-i`, above, is called a flag. It tells the `ssh` program that the string following it is the path to a
private key that should be used to authenticate with the remote host. The last string in the command
is a combination of the username to log in with, and hostname of the remote system, seperated by the `@` symbol.

## Windows Only
#### Install Putty
 1. Download http://the.earth.li/~sgtatham/putty/latest/x86/putty.zip
 2. Unzip
 3. Run `PUTTY.EXE`
 4. Enter the username and hostname of the EC2 instance that you would like to log into (e.g. username@myhost.foo.com)
 4. Generate a Putty key if you have not already (below)
 5. In the left-hand pane of the Putty login window, navigate to `Connection` -> `SSH` -> `Auth`
 6. In the `Auth` configuration window, select your Putty key (ppk) file.

#### Generate your Putty Key (.ppk)
 1. In the putty directory that you unziped, run `PUTTYGEN.EXE`
 2. Click the `Load` button, and select your personal key file.
 3. Click `Save Private Key`

## Creating EC2 instances

```knife ec2 server create -I ami-f75b329e -f t1.micro -S hackademy```

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
The Error at the end is OK!
