# To download:

FreeDos 1.4 or newer (Full USB)

    https://www.freedos.org/download/


Then you can follow the procedure at [PROCEDURE.md](PROCEDURE.md)



## Sources of this repository content:

### Firmware to flash to HBA330 (should be the same for r730xd/r740xd)

    For H330 Adapter:

        https://www.dell.com/support/home/fr-fr/drivers/driversdetails?driverid=nknvc&oscode=w12r2&productcode=poweredge-r740xd

    For H330 Mini:

        https://www.dell.com/support/home/fr-fr/drivers/driversdetails?driverid=124x2&oscode=wst14&productcode=poweredge-r740xd



### Tools from Broadcom

    MegaCli.exe and Megarec.exe (or Megarec3.exe in some tutorial):

        https://www.broadcom.com/support/knowledgebase/1211161499804/lsi-pre-boot-usb-tool-download

    Notes:
        - MegaCli.exe is from "boot/LSI/FW/MegaCli.exe".  
        - Megarec.exe is just the file "boot/LSI/FW/Recover/Megacli.exe" renamed like this, nothing more complicated (could not find this info online!).

<!-- -->

    sas3flsh:

        https://docs.broadcom.com/docs/Installer_P16_for_MSDOS_and_Windows.zip



### Other files

    smc3108.rom (taken from Abacus Electric, maybe better (official) source could be found:

        https://ftp.abacus.cz/support/FW/STORAGE/SUPERMICRO/FIRMWARE_SM_3108/4.270.00-3972/

    sbrempty.bin:

        % od -t x1 sbrempty.bin
        0000000    00  00  00  00  00  00  00  00  00  00  00  00  00  00  00  00
        *
        0000220    00  00  00  00  00  00  00  00  ff  ff  ff  ff  ff  ff  ff  ff
        0000240    ff  ff  ff  ff  ff  ff  ff  ff  ff  ff  ff  ff  ff  ff  ff  ff
        *
        0000400

