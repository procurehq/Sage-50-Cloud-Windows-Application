# Sage50cloud Integration Client Installation

This document details the steps to follow to install the ProcureHQ Windows Service on the client’s machine.

This document is Version 1 created on 19 February 2020.

## Installation Prerequisites

#### Machine Availability

This program has to be installed on a machine which will have an active connection to the Sage 50 database. The connection between ProcureHQ and your Sage Accounts software will only work if the machine is turned on and the service is configured and running in the background. 

#### Sage50cloud user

It is recommend that a new user be created that will be used by the ProcureHQ integration component. This allows Sage50cloud to monitor usage. The recommended name is “sdo”. Make a note of the password.

#### Sage50cloud files location

Make a note of the Sage50cloud files location. This is typically in the form

`C:\PROGRAMDATA\SAGE\ACCOUNTS\2020\Business\ACCDATA\`

## Installation Procedure


1. Download the latest release and unzip into a permanant directory. (*Ensure the zip file is unlocked. Right click > Properties > Unlock*)

2. You will need to get your ProcureHQ authorisation token from your account here: https://app.procurehq.com/settings#/api

3. SDO Type Lib Registration - 

   For the Windows Service to work the Type Lib needs to be registered.

   This MUST be run as Administrator. Right click the .EXE and select Run as Administrator.

   Enter the full tlb path. And press Register.

   Run VBRegTLB6.exe

   

   | **Sage 50 Version** | **TLB Location**                  |
   | ------------------- | --------------------------------- |
   | V24                 | C:\Windows\SysWOW64\SdoENG240.tlb |
   | V26                 | C:\Windows\SYSWOW64\SDOENG260.tlb |

   

4. SDO Activation - V24.2 and below only

   Sage SDO needs to be activated for it to work. The following article (<https://my.sage.co.uk/public/help/askarticle.aspx?articleid=9342>) details the full Sage description.

   A summary for Sage Accounts V24 is given below. The following Serial Number and Activation Key need to be entered into Sage V24.

   Please get the activation keys from ProcureHQ.

    To enter your Sage Data Objects activation information

   \1. On the menu bar click **Tools** then click **Activation** and click **Enable 3rd Party Integration**.

   **Note:** If the **Tools** menu doesn't appear, log on to Sage Accounts using the **MANAGER** logon.

   \2.    Enter your Sage Data Objects serial number and activation key then click **Continue**.



   

### Install the Windows Service

In Windows Explore determine the location of the InstallUtil.exe utility. This normally in

C:\Windows\Microsoft.NET\Framework\v4.0.30319\

Open a command window. This must be opened as an Administrator.

In the command window navigate to the directory where the ProcureHQ files were installed.

Run the command

{location of install utility}\InstallUtil.exe -u ProcureHQSage5025.exe

For example.

C:\Windows\Microsoft.NET\Framework\v4.0.30319\InstallUtil.exe ProcureHQSage5025.exe

   

To uninstall the service run the InstallUtile.exe command with the –u. For example

C:\Windows\Microsoft.NET\Framework\v4.0.30319\InstallUtil.exe -u ProcureHQSage5025.exe

### Configure the Windows Service

Add a desktop link to ProcureHQConfig.exe in the installation directory.

Open ProcureHQConfig and the screen will be displayed

   

Enter and Apply the configuration settings.

### Start the Windows Service

Type Services in the Windows search bar.

Search for ProcureHQ as shown below

  

Right click and the select Properties



Change “Startup type” to Automatic. Then click Apply

The click Start.

## Check Installation

In the installation directory open ServiceLog.txt file and check if there are any errors.

In ProcureHQ start the Invoice processing steps and ensure corresponding entries appear in Sage50cloud. This may take a few minutes.

### Update Process

1. Download Latest Update

2. Stop Running Service 

3. Backup the existing 

   `ProcureHQService.config`

4. Uninstall Service

   `C:\Windows\Microsoft.NET\Framework\v4.0.30319\InstallUtil.exe -u ProcureHQSage5025.exe`

5. Install Service (Reconfigure "Run As Permission" if you are using a network drive which requires authentication.) 

   `C:\Windows\Microsoft.NET\Framework\v4.0.30319\InstallUtil.exe ProcureHQSage5025.exe`

6. Copy back up file to existing directory

   `ProcureHQService.config`

7. Restart Service

   

   ## Logging

   When logging is switched “On” information is written to the SystemLog.txt in the installation directory.

   Logging should be switched “On” when verifying the installation and initial processing. It should be switched “Off” during regular operation.

   ### 



