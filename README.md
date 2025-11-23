# Files to download:

Firmware for H330 Adapter or your specific card.
Here for H330 Adapter (should be the same for r730xd/r740xd):

    https://www.dell.com/support/home/fr-fr/drivers/driversdetails?driverid=nknvc&oscode=w12r2&productcode=poweredge-r740xd

FreeDos 1.4 or newer (Full USB)

    https://www.freedos.org/download/

MegaCli.exe and Megarec.exe (or Megarec3.exe in some tutorial).
MegaCli.exe is from "boot/LSI/FW/MegaCli.exe".
Megarec.exe is just the file "boot/LSI/FW/Recover/Megacli.exe" renamed like this, nothing more complicated (could not find this info online!).

    https://www.broadcom.com/support/knowledgebase/1211161499804/lsi-pre-boot-usb-tool-download

sas3flsh:

    https://docs.broadcom.com/docs/Installer_P16_for_MSDOS_and_Windows.zip

smc3108.rom (taken from Abacus Electric, maybe better (official) source could be found:

    https://ftp.abacus.cz/support/FW/STORAGE/SUPERMICRO/FIRMWARE_SM_3108/4.270.00-3972/

sbrempty.bin:
```
% od -t x1 sbrempty.bin
0000000    00  00  00  00  00  00  00  00  00  00  00  00  00  00  00  00
*
0000220    00  00  00  00  00  00  00  00  ff  ff  ff  ff  ff  ff  ff  ff
0000240    ff  ff  ff  ff  ff  ff  ff  ff  ff  ff  ff  ff  ff  ff  ff  ff
*
0000400
```

Just dd freedos to the key and mount the key (image has enough left space to hold the files we will copy).
Then copy the files from "to_put_on_key"

Then boot into FreeDos and follow this procedure.

# PROCEDURE

## 1. SAVE INFO (SAS Address and Serial number)
megacli -adpallinfo -a0 > h330info.txt

## 2. Optional: Flash temp ROM
megacli -adpfwflash -f smc3108.rom noverchk -a0
reboot

(wait 3-5 min until "No adapter")

## 3. Erase flash
megarec -writesbr 0 sbrempty.bin
megarec -cleanflash 0

reboot

## 4. Verify erased
sas3flsh -list

## 5. Flash HBA330 from Dell website for H330 Adapter or your specific model
sas3flsh -o -f SAS_HBA330_ADP_SF.fw -b mptx64-sas3-sb.rom

## 6. Program SAS address and Serial number (from file save at step 1)
sas3flsh -c 0 -o -sasadd YOUR_16_CHAR_ADDRESS -tracer SERIAL_ID

## 7. Verify
sas3flsh -listall