Step by step setting up an imaging system.


1. Get an install.wim file. (this is the image that will be deployed via MDT/WDS)
  you can do this by grabbing the D:\sources\install.esd from a win10 iso and converting it with teh dism tool
  
  View the index you want with 
    dism /Get-WimInfo /WimFile:install.esd
  
  Do the actual Conversion
    dism /export-image /SourceImageFile:install.esd /SourceIndex:1 /DestinationImageFile:install.wim /Compress:max /CheckIntegrity

2. Drivers
  first install an image and update the physical hardware to the latest firmware.
  Install windows on that image.
  Update to the latest drivers.
  Export the drivers to be used in the MDT image.
    export-windowsdriver
 
 3.
