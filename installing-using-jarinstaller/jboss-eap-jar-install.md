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

Prompt a name, e.g. "jboss-eap-install-file" for the installation file you can use for the subsequence silent and automated installations without the need to use the GUI
![Prompt a name for the installation file](images/select-folder-for-install-file.png?raw=true)

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

