# Installing JBoss EAP 7.4 through jar installer package

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