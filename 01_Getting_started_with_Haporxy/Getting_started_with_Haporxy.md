# 1.0 Introduction 
To get started with Haproxy, you first need to install it
on a system and learn some basics. In this chapter, you will learn how to install
Haproxy, where the main configuration files are, and commands.
You will also learn how to verify your installation and make requests to the default
server.

# 1.1 Installing on Debian/Ubuntu

## Problem
You need to install Haproxy on a Debian or Ubuntu machine.

## Solution

### Install with packege manager

to install Haproxy on a Debian/Ubuntu you can use the the os
package manager.
```bash
sudo apt install haproxy
```
### Install the Latest HAProxy Using a PPA
Head over to [haproxy.debian.net](https://haproxy.debian.net), where you can select the install instructions for your OS. At the time of this writing, the latest version was 2.9. Select the options for Ubuntu Focal (20.04 LTS) (long-term support) and HAProxy 2.8 (LTS). This will bring you to a page listing the commands you need to run:
```bash
sudo apt-get install --no-install-recommends software-properties-common
sudo add-apt-repository ppa:vbernat/haproxy-2.8 -y
```
The first command installs the software-properties-common package which helps you manage any PPAs you install. It’s probably already installed, but running it again ensures that it’s available. The second command puts the PPA into the list of software sources.

We’re now ready to install the very latest HAProxy:
```bash
sudo apt-get install haproxy=2.8.\*
```

# 1.2 Installing on RedHat/CentOS

## Problem

You need to install NGINX Open Source on RedHat or CentOS.

### Update Your System

Open your terminal or SSH into your server and enter the following command:
```bash
sudo yum update -y
```
This command will fetch the latest versions of installed packages and upgrade them. The -y flag automatically answers ‘yes’ to any prompts, streamlining the process.

### Add the HAProxy Repository

HAProxy, while popular, isn’t available in the default CentOS repositories. To access the latest version of HAProxy, you’ll need to add the EPEL (Extra Packages for Enterprise Linux) repository, which contains additional packages for enterprise Linux.

To add the EPEL repository in your terminal, type the following command:
```bash
sudo yum -y install epel-release
```
This command installs the EPEL repository package. Once this is done, your system will have access to many more packages, including the latest version of HAProxy.

### Install HAProxy
With the EPEL repository added to your system, you’re now ready to install HAProxy.

Still in your terminal, enter the following command:
```bash
sudo yum -y install haproxy
```

# 1.3 Verifying Your Installation

## Problem
You want to validate the HAProxy installation and check the version.

## Solution
You can verify that HAProxy is installed and check its version by using the following
command:
```bash
haproxy -v
HAProxy version 2.8.5-1ppa1~focal 2023/12/09 - https://haproxy.org/
Status: long-term supported branch - will stop receiving fixes around Q2 2028.
Known bugs: http://www.haproxy.org/bugs/bugs-2.8.5.html
Running on: Linux 5.15.0-94-generic 104~20.04.1-Ubuntu SMP Tue Jan 16 13:34:09 UTC 2024 x86_64
```

# 1.4 KeyFiles, Directory, and Commands

## Problem
You need to understand the important HAProxy directories and commands.

## Solution

### HAProxy files and directories
`/etc/haproxy/`
The `/etc/haproxy/` directory is the default configuration root for the haproxy.
Within this directory you will find configuration files that instruct HAProxy on
how to behave.

`/etc/haproxy/haproxy.cfg`
The HAProxy service uses the `/etc/haproxy/haproxy.cfg` file as its default configuration entry point. This configuration file configures global variables for timeout, logging, errorfile, and other global variables. You can click this [link](https://www.haproxy.com/documentation/haproxy-configuration-manual/2-8r1/) to view additional information.

### HAProxy commands

**Starting HAProxy**:
```bash
haproxy -f /path/to/haproxy.cfg
```

**Querying HAProxy Status**:
```bash
haproxy -vv
```

**Stats Socket**:
```bash
echo "disable server <backend_name>/<server_name>" | socat /var/run/haproxy.sock stdio
```
