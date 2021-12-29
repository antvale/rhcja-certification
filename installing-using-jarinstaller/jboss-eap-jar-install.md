# Installing JBoss EAP 7.4 through jar installer with GUI

```console
rhcja-lab user$ sudo java -jar jboss-eap-7.4.0-installer.jar
```

Select English language from popup dropdown list and click "OK" button

![Language Selection](images/language-selection.png?raw=true)

Read fastly the Lincensig Agreement and agree the conditions, then click "NEXT" button

![Agree License](images/licensing-agreement.png?raw=true)

prompt the installation path, usially /opt/jboss-eap-7.4

> **⚠ WARNING: keyboard language**  
Note that in some case the keyboard language swithces to ENG, so you shout type the key "-" for "/" and "'" for "-", instead "." is the same in both IT and ENG language!**

![Prompt the installation path](images/installation-path.png?raw=true)

Leave the default options and go to "NEXT" step

![Component selection](images/component-selection.png?raw=true)

Enter jbossadm user with JBoss@RedHat123 pwd and click "NEXT" button

![Create the jboss admin user to access the EAP Management Console](images/create-jboss-admin-user.png?raw=true)

Check installation summary and go to previous steps if needed
![Check the installation overview and go to previous steps if required](images/installation-overview.png?raw=true)

Installer starts the installation of selected components and on complete shows the summary as follow, click "NEXT"
![Component installation summary](images/component-installation.png?raw=true)

Select "Perform default configuration" and click "NEXT"
![Configure runtime env](images/configure-runtime-environment.png?raw=true)

![Processing completed](images/processing-completed.png?raw=true)

Select "Generate installation script and properties files"

take note of the uninstall forlder when need to uninstall jboss EAP

![Installation successfully completed](images/installation-successfully.png?raw=true)

Prompt a name, e.g. "jboss-eap-7.4-install-file" for the installation file you can use for the subsequence silent and automated installations without the need to use the GUI
![Prompt a name for the installation file](images/select-folder-for-install-file.png?raw=true)

> **Note:** The filename has been modified from "jboss-eap-install-file" to "jboss-eap-7.4-install-file"

Click "DONE" to complete the installation
![Prompt a name for the installation file](images/install-file-generated-properly.png?raw=true)

# Installing JBoss through jar installer without GUI

Required: JBoss configuration file generated to previous step

These steps automate the installation process being not required to prompt manually stuff during the installation.

> **WARNING:** Use sudo to open both jboss-eap-install-file.xml and jboss-eap-install-file.xml.variables files

```console
-rw-r--r--   1 root  wheel      30 28 Dic 10:19 jboss-eap-install-file.xml.variables
-rw-------   1 root  wheel    3362 27 Dic 23:23 jboss-eap-install-file.xml
```

Go to installation path "/opt/jboss-eap-7.4" and open the installation config file:

```console
sudo less jboss-eap-install-file.xml
```

Check the presence of the lines (find by 'admin')

```javascript
<userInput>
    <entry key="adminUser" value="jbossadm"/>
    <entry autoPrompt="true" key="adminPassword"/>
</userInput>
```

Go to file jboss-eap-install-file.xml.variables and enter the pwd in the attribute "adminPassword", should be the only one attribute of this file

```console
sudo vi jboss-eap-install-file.xml.variables
```

enter the password:
adminPassword=JBoss@RedHat123

Start the silent installation. This doesn't require to any human interaction during the process.

```console
[azureuser@vm-rhel-rhjca-8 ~]$ sudo java -jar jboss-eap-7.4.0-installer.jar jboss-eap-install-file.xml
Checking for corresponding .variables file
Variables file detected: /home/azureuser/jboss-eap-install-file.xml.variables
[ Starting automated installation ]
Read pack list from xml definition.
Try to add to selection [Name: Red Hat JBoss Enterprise Application Platform and Index: 0]
Try to add to selection [Name: AppClient and Index: 1]
Try to add to selection [Name: XMLs and XSDs and Index: 2]
Try to add to selection [Name: Modules and Index: 3]
Try to add to selection [Name: Welcome Content and Index: 4]
Modify pack selection.
[ Starting to unpack ]
[ Processing package: Red Hat JBoss Enterprise Application Platform (1/5) ]
[ Processing package: AppClient (2/5) ]
[ Processing package: Docs (3/5) ]
[ Processing package: Modules (4/5) ]
[ Processing package: Welcome Content (5/5) ]
[ Unpacking finished ]
[ Starting processing ]
Starting process Logging installation information (1/3)
IzPack variable state written to /opt/jboss-eap-7.4/installation/InstallationLog.txt
Starting process Adding admin user (2/3)
Starting process Cleanup extraneous folders and tepmorary files (3/3)
[ Processing finished ]
[ Writing the uninstaller data ... ]
[ Automated installation done ]
```

Check the forlder "/opt/jboss-eap-7.4" has been created successfully with all the required subfolders and files as specified in the installation config file.

```console
azureuser@vm-rhel-rhjca-8 jboss-eap-7.4]$ ls -alt
total 580
drwxr-xr-x. 14 root root   4096 Dec 28 09:38 .
drwxr-xr-x.  2 root root   4096 Dec 28 09:38 installation
drwxr-xr-x.  2 root root   4096 Dec 28 09:38 uninstaller
drwxr-xr-x.  4 root root   4096 Dec 28 09:38 welcome-content
drwxr-xr-x.  3 root root   4096 Dec 28 09:38 modules
drwxr-xr-x.  5 root root   4096 Dec 28 09:38 docs
drwxr-xr-x.  3 root root   4096 Dec 28 09:38 appclient
drwxr-xr-x.  4 root root   4096 Dec 28 09:38 bin
drwxr-xr-x.  2 root root   4096 Dec 28 09:38 .installation
drwxr-xr-x.  3 root root   4096 Dec 28 09:38 .well-known
drwxr-xr-x.  4 root root   4096 Dec 28 09:38 domain
drwxr-xr-x.  6 root root   4096 Dec 28 09:38 standalone
drwxr-xr-x.  3 root root   4096 Dec 28 09:38 migration
drwxr-xr-x.  4 root root   4096 Dec 28 09:38 ..
-rw-r--r--.  1 root root    419 Jun 23  2021 JBossEULA.txt
-rw-r--r--.  1 root root  26530 Jun 23  2021 LICENSE.txt
-rw-r--r--.  1 root root 496975 Jun 23  2021 jboss-modules.jar
-rw-r--r--.  1 root root     65 Jun 23  2021 version.txt
```

## Set env variables

Set JBOSS_HOME as env variable. Open in edit the file "/home/azureuser/.bashrc"

```console
vi /home/azureuser/.bashrc
```

You should see something similar to:

```console
# .bashrc
  
# Source global definitions
if [ -f /etc/bashrc ]; then
        . /etc/bashrc
fi

# User specific environment
PATH="$HOME/.local/bin:$HOME/bin:$PATH"
export PATH

# Uncomment the following line if you don't like systemctl's auto-paging feature:
# export SYSTEMD_PAGER=

# User specific aliases and functions
```

Add at the end of the file (after the line # User specific aliases and functions") the following lines

```console
JBOSS_HOME=/opt/jboss-eap-7.4
PATH=$PATH:$JBOSS_HOME/bin
export JBOSS_HOME PATH
```
> **WARNING:** To avoid mistake use always the **$JBOSS_HOME** in place of the absolute path "/opt/jboss-eap-7.4"

Logout and login to apply the above changes and then execute the below shells. It works if the outputs show the right path "/opt/jboss-eap-7.4" for JBOSS_HOME and the absolute path where the exec file "standalone.sh" is located, that's, "/opt/jboss-eap-7.4/bin/standalone.sh"

```console
[azureuser@vm-rhel-rhjca-8 ~]$ echo $JBOSS_HOME
/opt/jboss-eap-7.4
[azureuser@vm-rhel-rhjca-8 ~]$ which standalone.sh
/opt/jboss-eap-7.4/bin/standalone.sh
```

Create the system user with "-r" option preventing it from login/logout in the system:

```console
[azureuser@vm-rhel-rhjca-8 ~]$ sudo useradd -r jboss
```

Check the corrispondending id is less than 1000

```console
[azureuser@vm-rhel-rhjca-8 ~]$ id jboss
uid=990(jboss) gid=986(jboss) groups=986(jboss)
```

Make this user owner of the JBOSS_HOME folder and all the files it contains. Use sudo because the /opt/jboss-eap-7.4 folder required root privileges 

```console
[azureuser@vm-rhel-rhjca-8 ~]$ sudo chown -R jboss:jboss $JBOSS_HOME
```

<mark>Check the owner has been applied properly</mark>

```console
[azureuser@vm-rhel-rhjca-8 jboss-eap-7.4]$ ls -alt
total 580
drwxr-xr-x. 14 jboss jboss   4096 Dec 28 09:38 .
drwxr-xr-x.  2 jboss jboss   4096 Dec 28 09:38 installation
drwxr-xr-x.  2 jboss jboss   4096 Dec 28 09:38 uninstaller
drwxr-xr-x.  4 jboss jboss   4096 Dec 28 09:38 welcome-content
drwxr-xr-x.  3 jboss jboss   4096 Dec 28 09:38 modules
drwxr-xr-x.  5 jboss jboss   4096 Dec 28 09:38 docs
drwxr-xr-x.  3 jboss jboss   4096 Dec 28 09:38 appclient
drwxr-xr-x.  4 jboss jboss   4096 Dec 28 09:38 bin
drwxr-xr-x.  2 jboss jboss   4096 Dec 28 09:38 .installation
drwxr-xr-x.  3 jboss jboss   4096 Dec 28 09:38 .well-known
drwxr-xr-x.  4 jboss jboss   4096 Dec 28 09:38 domain
drwxr-xr-x.  6 jboss jboss   4096 Dec 28 09:38 standalone
drwxr-xr-x.  3 jboss jboss   4096 Dec 28 09:38 migration
drwxr-xr-x.  4 root  root    4096 Dec 28 09:38 ..
-rw-r--r--.  1 jboss jboss    419 Jun 23  2021 JBossEULA.txt
-rw-r--r--.  1 jboss jboss  26530 Jun 23  2021 LICENSE.txt
-rw-r--r--.  1 jboss jboss 496975 Jun 23  2021 jboss-modules.jar
-rw-r--r--.  1 jboss jboss     65 Jun 23  2021 version.txt
```

Start jboss as standalone server

```console
sudo -u jboss /opt/jboss-eap-7.4/bin/standalone.sh
```

Standalone server is started successfully if you see the below line

```console
09:59:31,749 INFO  [org.jboss.as] (Controller Boot Thread) WFLYSRV0025: JBoss EAP 7.4.0.GA (WildFly Core 15.0.2.Final-redhat-00001) started in 13515ms - Started 317 of 556 services (343 services are lazy, passive or on-demand)
```

To check if the server is up and running go to browser and open the link http://localhost:8080, you should see the welcome page of Jboss saying "Your Red Hat JBoss Enterprise Application Platform is running" and showing the link for Admin console or alternatively use curl

```console
curl http://localhost:8080
```

To stop jboss press CTRL+C to stop the current process running in the console.

```console
10:11:02,203 INFO  [org.jboss.as] (MSC service thread 1-1) WFLYSRV0050: JBoss EAP 7.4.0.GA (WildFly Core 15.0.2.Final-redhat-00001) stopped in 163ms
```

## Configure the jboss starup script

In "/opt/jboss-eap-7.4/bin/init.d" there are 2 files
```console
[azureuser@vm-rhel-rhjca-8 init.d]$ ls -alt
total 20
drwxr-xr-x. 4 jboss jboss 4096 Dec 28 09:38 ..
drwxr-xr-x. 2 jboss jboss 4096 Dec 28 09:38 .
-rwxr-xr-x. 1 jboss jboss 5009 Jun 23  2021 jboss-eap-rhel.sh
-rw-r--r--. 1 jboss jboss  866 Jun 23  2021 jboss-eap.conf
```

Edit the "jboss-eap.conf":
```console
[azureuser@vm-rhel-rhjca-8 init.d]$ sudo -u jboss vi jboss-eap.conf
```
and change the following properties:
```console
# uncomment the JAVA_HOME and set with the right jdk version
# Go to /etc/alternatives to find the java sdk 1.8.0
JAVA_HOME="/etc/alternatives/java_sdk"

# uncomment JBOSS_HOME property and set it with the right path
JBOSS="/opt/jboss-eap-7.4"

#uncomment JBOSS_USER and set the right one
JBOSS_USER=jboss

# Just uncomment JBOSS_MODE
JBOSS_MODE=standalone

# Just uncomment JBOSS_CONFIG
JBOSS_CONFIG=standalone.xml

# Just uncomment JBOSS_CONSOLE_LOG
JBOSS_CONSOLE_LOG="/var/log/jboss-eap/console.log"
```

Copy the file "jboss-eap.conf" to "/etc/default"

```console
sudo cp /opt/jboss-eap-7.4/bin/init.d/jboss-eap.conf /etc/default/
```

<mark>Copy the file "jboss-eap-rhel.sh" to "/etc/init.d" renaming it in "jboss-eap"
</mark>

```console
sudo cp /opt/jboss-eap-7.4/bin/init.d/jboss-eap-rhel.sh /etc/init.d/jboss-eap
```

Make the file executable by owner, group and others
```console
sudo chmod 755 /etc/init.d/jboss-eap.sh
```

Reload systemctl, enable the service jboss-eap and start it:
```console
[azureuser@vm-rhel-rhjca-8 init.d]$ sudo systemctl daemon-reload
[azureuser@vm-rhel-rhjca-8 init.d]$ sudo systemctl enable jboss-eap.sh
jboss-eap.sh.service is not a native service, redirecting to systemd-sysv-install.
Executing: /usr/lib/systemd/systemd-sysv-install enable jboss-eap.sh
[azureuser@vm-rhel-rhjca-8 init.d]$ sudo systemctl start jboss-eap
```

If something has been wrong prompt (to know what happened)
```console
[azureuser@vm-rhel-rhjca-8 init.d]$ sudo systemctl status jboss-eap
```
If you got a permission denied error then likely you shoult configure SELinux properly, see next steps
```console
Dec 29 13:35:10 vm-rhel-rhjca-8.0 jboss-eap[4127]: Starting jboss-eap: /etc/rc.d/init.d/jboss-eap: line 104: /var/log/jboss-eap/console.log: Permission denied
Dec 29 13:35:10 vm-rhel-rhjca-8.0 jboss-eap[4127]: /etc/rc.d/init.d/jboss-eap: line 113: /var/log/jboss-eap/console.log: Permission denied
Dec 29 13:35:10 vm-rhel-rhjca-8.0 jboss-eap[4127]: /
```

To configure SELinux:
```console
sudo ausearch -c 'jboss-eap' --raw | sudo audit2allow -M jboss-eap
******************** IMPORTANTE ***********************
Per rendere attivo questo pacchetto di politiche, eseguire: semodule -i jboss-eap.pp

[azureuser@vm-rhel-rhjca-8 run]$ sudo semodule -X 300 -i jboss-eap.pp
```

Then start again jboss-eap (now it would work)
```console
[azureuser@vm-rhel-rhjca-8 init.d]$ sudo systemctl start jboss-eap
```
Check with the browser or curl.