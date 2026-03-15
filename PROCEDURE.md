# PROCEDURE

Just dd freedos to the key and mount the key (image has enough left space to hold the files we will copy).
Copy the files you need from "to_put_on_key" (depending on your card).

Then boot into FreeDos and follow those steps:


### 1. SAVE INFO (SAS Address and Serial number)

    megacli -adpallinfo -a0 > h330info.txt

### 2. Optional: Flash temp ROM

    megacli -adpfwflash -f smc3108.rom noverchk -a0

    reboot

    (wait 3-5 min until "No adapter")

### 3. Erase flash

    megarec -writesbr 0 sbrempty.bin
    megarec -cleanflash 0

    reboot

### 4. Verify erased

    sas3flsh -list

### 5. Flash HBA330 from Dell website for H330 Adapter or your specific model

    sas3flsh -o -f SAS_HBA330_ADP_SF.fw -b mptx64-sas3-sb.rom

### 6. Program SAS address and Serial number (from file save at step 1)

    sas3flsh -c 0 -o -sasadd YOUR_16_CHAR_ADDRESS -tracer SERIAL_ID

### 7. Verify

    sas3flsh -listall