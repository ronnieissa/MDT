Step by step setting up an imaging system.

To capture an updated and clean OS from a VM disk.
  Mount the vm Disk on the host OS.
  Run this command
    dism /capture-image /imagefile:<imag-path> /capturedir:<source_drive> /name:<name> /description:<description>
  
 IF USING ISO, see below
  
 1. Get an install.wim file. (this is the image that will be deployed via MDT/WDS)
  you can do this by grabbing the D:\sources\install.esd from a win10 iso and converting it with teh dism tool
  
  View the index you want with 
    dism /Get-WimInfo /WimFile:install.esd
  
  Do the actual Conversion
    dism /export-image /SourceImageFile:install.esd /SourceIndex:1 /DestinationImageFile:install.wim /Compress:max /CheckIntegrity
    
  Import the WIM file into the deployment share
    Import-Module "C:\Program Files\Microsoft Deployment Toolkit\bin\MicrosoftDeploymentToolkit.psd1"
    New-PSDrive -Name "DS001" -PSProvider MDTProvider -Root "C:\DeploymentShare"
    import-mdtoperatingsystem -path "DS001:\Operating Systems" -SourceFile "C:\win10.wim" -DestinationFolder "win10" -Move -Verbose

2. Drivers
  first install an image and update the physical hardware to the latest firmware.
  Install windows on that image.
  Update to the latest drivers.
  Export the drivers to be used in the MDT image.
    export-windowsdriver
 
 3. Import the w
