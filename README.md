this is a modded fork of Joepool's repo in hopes to add Mac OS 12 support the opencore pkg has been updated from 0.7.5---->0.8.4 amoung other tweaks that will be outlined in my releases
# Hackintosh-HP-Z420-OpenCore
### Do not just copy this EFI and expect it to work
Hackintosh EFI for HP Z420 Workstation - Tested on Catalina and Big Sur   
# Setup
This EFI is setup for debugging, it uses the debug version of OpenCore, and has logging/verbose enabled.   
### Required BIOS Settings
Version 3.96 (Latest)    
SATA Mode - AHCI   
Enable Legacy ACPI CPU Tables   
### Create USB Installer
https://dortania.github.io/OpenCore-Install-Guide/installer-guide/ - Follow this guide to add macOS to the USB.   
Mount the EFI Partition.   
Copy the EFI files from the release zip file into your EFI partition.    
You will need to generate a MacPro6,1 SMBIOS using [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS).  
For any GPU other than the NVidia Quadro K4000 you can remove the SSDT-GPU-SPOOF.aml, unless it is natively unsupported. In this case, you will have to edit the SSDT   
Follow [This Guide](https://dortania.github.io/Getting-Started-With-ACPI/Universal/spoof.html) to edit it. Do not change the Device ID, but you need to change the Model and PCIe Root. (Explained in the guide)  
Boot the USB installer and install macOS.  
### Post Install
https://dortania.github.io/OpenCore-Post-Install/ - Steps are outlined in this guide.   
Mount your drives EFI partition and copy the contents of your USB installer's EFI partition to your drives EFI Partition.   
Convert fron the debug version of opencore to the release version, cleanup logging etc. Follow [This Guide](https://dortania.github.io/OpenCore-Post-Install/cosmetic/verbose.html#macos-decluttering).   
Follow any other steps you would like to complete your hackintosh. 
### Audio
I have now managed to get Audio fully working with AppleALC. This means that audio will work on MacOS versions above 11.3.  
Credit to @BillDH2k for finding the IRQ conflicts issue and a solution. 
### Important when Updating to OC 0.6.6
If you have previously installed this with OpenCore 0.6.5 or older and update to OpenCore 0.6.6, there are a few thing you will need to do. (If are are doing a fresh installation ignore this)   
As bootstrap has been removed you will not be able to boot OC 0.6.6 without resetting your NVRAM as it will try to boot bootstap.    
Before you first boot with 0.6.6, reset your NVRAM from the opencore boot picker(If the option doesn't show up, press the spacebar), then for the first time you will have to boot the `EFI/BOOT/BOOTx64.efi` option - after firdt boot it should be back to normal. See [this page for more info](https://dortania.github.io/OpenCore-Post-Install/multiboot/bootstrap.html#updating-bootstrap-in-0-6-6)   
If you use OpenCanopy (Graphical boot picker) you will also have to update your Resources folder, which can be done from [here](https://github.com/acidanthera/OcBinaryData).   
# My System
Intel Xeon E5-1650 v2 CPU  
Radeon RX 590 (Gigabyte)
32GB ECC DDR3   
# Issues
USB3 - The Z420 uses a Texas Instruments USB 3 Controller which is unsupported in MacOS - I have solved this by using [This PCIe expansion card](https://www.amazon.co.uk/gp/product/B00JEVLEFQ/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1) which can fix the two front pannel USB3 ports and give two extra USB3 ports in the rear. The Unsupported USB 3.0 controller means that your Install USB must be connected to a USB 2.0 port. If it is connected to a USB 3.0 port you will get the error `Still waiting for root device`    
DRM - My GPU is incompatable so DRM will never work for me, most GPU's have support, see [this page]()   
Sleep doesn't work - you need to disable it inside of macOS.  
If you have any other issues, feel free to open a GitHub issue and I will do my best to help!   
