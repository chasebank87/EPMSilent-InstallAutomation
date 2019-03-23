
# Distributed HFM | Two Server Environment
* Time: ___1 Hour___
* Version ___11.1.2.4.900___
* Status: ___Tested Working___
* Note: ___Interactive mode not supported yet for multiple server deployments. Silent only___



### Steps:
  #### Foundation Server: (First)
  1. Clone repo to a folder on your ***Foundation Server*** __(make sure it is as close to the base drive as possible, or you may get file path too long errors)__
  2. Unblock the __three__ powershell files in the powershell folder. __(Right click file.. Select Properties.. Click unblock)__
  3. Open Powershell as administrator
  4. Set Execution policy to __Unrestricted__
  ```powershell
  Set-ExecutionPolicy Unrestricted
  ```
  5. Browse to the powershell path in the folder you cloned
  ```powershell
  cd c:\EPM\InstallAutomation\Powershell
  ```
  6. To run the script in silent mode
  * Determine what products you want __(SOA: Tax, and FCM are not supported)__
  * Modify the following command to fit your needs:
```powershell
.\start.ps1 -superSilentAll -installIIS $true -installNetFrame $true -install7zip $true -installnotepadplus  $true -installfirefox $true -installepm $true -version900 -epmPath c:\Oracle\Middleware -installFoundation $true -installEssbase $false -installFR $true -installHFM $true -installfdm $true -dbServer sql.domain.local -dbPort 1433 -dbUser hypadmin -dbPassword Password! -wkspcAdmin admin -wkspcAdminPassword Password! -weblogicAdmin epm_admin -weblogicPort 7001 -weblogicHostname foundation.domain.local -wkspcPort 19000 -epmDomain EPMSystem -foundationDB EPMS_FND -epmaDB EPMS_BPM -calcDB EPMS_CAL -frDB EPMS_HFR -hfmDB EPMS_HFM -fdmDB EPMS_FDM -strategic $false -distributedHFM $true -remoteDeployment $false
```
  * The difference with this command are the switches -distributedHFM, and -remoteDeployment. If you set -distributedHFM to $true, and -remoteDeployment to $false, willl only install ___(HFMWeb, and it won't configure)___ which is what you want to do on the foundation server.
  * If you dont want a product installed outside of HFM you can set the install to $false, and ommit the DB switch for that product. For instance if your client does not need __Essbase__ your command would look like this:
```powershell
.\start.ps1 -superSilentAll -installIIS $true -installNetFrame $true -install7zip $true -installnotepadplus  $true -installfirefox $true -installepm $true -version900 -epmPath c:\Oracle\Middleware -installFoundation $true -installFR $true -installHFM $true -installfdm $true -dbServer sql.domain.local -dbPort 1433 -dbUser hypadmin -dbPassword Password! -wkspcAdmin admin -wkspcAdminPassword Password! -weblogicAdmin epm_admin -weblogicPort 7001 -weblogicHostname foundation.domain.local -wkspcPort 19000 -epmDomain EPMSystem -foundationDB EPMS_FND -epmaDB EPMS_BPM -calcDB EPMS_CAL -hfmDB EPMS_HFM -frDB EPMS_HFR -fdmDB EPMS_FDM -strategic $false -distributedHFM $true -remoteDeployment $false
```
  * Reference the command line options on the home page of this repo for help
  #### HFM Server: (Second)
  1. Clone repo to a folder on your ***HFM Server*** __(make sure it is as close to the base drive as possible, or you may get file path too long errors)__
  2. Unblock the __three__ powershell files in the powershell folder. __(Right click file.. Select Properties.. Click unblock)__
  3. Open Powershell as administrator
  4. Set Execution policy to __Unrestricted_
  ```powershell
  Set-ExecutionPolicy Unrestricted
  ```
  5. Browse to the powershell path in the folder you cloned
  ```powershell
  cd c:\EPM\InstallAutomation\Powershell
  ```
  6. To run the script in silent mode
  * Determine what products you want __(SOA: Tax, and FCM are not supported)__ In the most common scenario only Essbase and Foundation would be installed on this standalone Essbase server.
  * Modify the following command to fit your needs: 
```powershell
.\start.ps1 -superSilentAll -installNetFrame $true -install7zip $true -installnotepadplus  $true -installfirefox $true -installepm $true -version900 -epmPath c:\Oracle\Middleware -installFoundation $true -installHFM $true -dbServer sql.domain.local -dbPort 1433 -dbUser hypadmin -dbPassword Password! -wkspcAdmin admin -wkspcAdminPassword Password! -weblogicAdmin epm_admin -weblogicPort 7001 -weblogicHostname foundation.domain.local -wkspcPort 19000 -epmDomain EPMSystem -foundationDB EPMS_FND -hfmDB EPMS_HFM -strategic $false -remoteDeployment $true -distributedHFM $true
```
  * The difference with this command from the one we did on the __Foundation Server__ is the -remoteDeployment swich, the values we provided for the install switches, and the DB switches we ommited
  * -remoteDeployment __$true__ tells the script that this is a remote server, and only installs __HFM__
  * Changing the -install switches to __$false__ tells the script not to install those products
  * Ommiting the different productDB switches tells the script not to try and configure the products we chose not to install

  #### Foundation Server: (Third)
  1. Run the configuration GUI
    * Start Menu
  2. Select Configure Web Server under Foundation
  3. Click next until completion
  
  ![alt text](https://github.com/chasebank87/EPMSilent-InstallAutomation/blob/master/Help/configureWeb.gif)
  
  
### See the above steps in action:

