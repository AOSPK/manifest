![KrakenProject](https://raw.githubusercontent.com/KrakenProject/official_devices/master/docs/banner.png)

### Requirements
- Around 75G disk space
- 20G or more usable internet
- A computer with at least 8G RAM running Linux or MacOS
- A brain

### Instructions
- Preparing the SERVER
    1. Make directory for the repo binary
        ```
        mkdir ~/bin
        ```
    2. Add directory for the repo binary to its path
        ```
        PATH=~/bin:$PATH
        ```
    3. Downloading repo binary and placing it in the proper directory
        ```
        curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
        ```
    4. Giving the repo binary the proper permissions
        ```
        chmod a+x ~/bin/repo
        ```
    5. Creating directory for where the KK repo will be stored and synced
        ```
        mkdir ~/kk
        cd ~/kk
        ```

- Preparing the ROM
    1. Make sure you have a build environment setup.
    2. Make a new directory, cd to it and run
        ```
        repo init -u https://github.com/KrakenProject/manifest -b pie
        ```
    3. Sync!
        ```
        repo sync -c -j$(nproc --all) --no-clone-bundle --no-tags --force-sync
        ```
    4. The ROM is ready! Get ready to prepare your device-specific.

- Preparing device
    1. Clone your tree repositories
        Example:
          ```
          git clone https://github.com/KrakenDevices/device_xiaomi_beryllium -b pie device/xiaomi/beryllium
          ```
    2. Move/copy your `<ROM>.mk` (Example: `lineage.mk` or `lineage_beryllium.mk`) file to `aosp_beryllium.mk`.
    3. Open this file and
        - Set PRODUCT_NAME to `aosp_<device>` (Example: `aosp_beryllium`)
        - For a Phone or tablet with a SIM Card, add
            ```
            # Inherit from Kraken vendor
            $(call inherit-product, vendor/aosp/config/common_full_phone.mk)
            ```
        - For a WiFi-only tablet, add
            ```
            # Inherit from Kraken vendor
            $(call inherit-product, vendor/aosp/config/common_full_tablet_wifionly.mk)
            ```
    4. Save and exit

- Building
    1. Run
        ```
        . build/envsetup.sh
        lunch aosp_<device>-userdebug
        make -j$(nproc --all) bacon
        ```
        Example:
        ```
        . build/envsetup.sh
        lunch aosp_beryllium-userdebug
        make -j$(nproc --all) bacon
        ```
        For detailed logs, use:
        ```
        make -j$(nproc --all) bacon 2>&1 | tee log.txt
        ```
    2. This will start compiling the build.
    3. Resolve errors if any and continue building.
    4. Remember to `make clobber && make clean` every now and then!

### Reporting compilation issues
- You can reach us at [**Telegram**](https://t.me/KrakenProject)
- For common porting related errors, visit [**Android Building Help**](https://t.me/AndroidBuildersHelp)
- Make sure you provide relevant logs, screenshots and details with all sources you used.

### Adding Support
- For adding your device to the list of supported devices, please reach us at [**GoogleForms**](https://forms.gle/AKinLpdy8VELaefE6) with your device tree and previous works.

Credits
-------
 * [**AOSP**](https://android.googlesource.com)
 * [**AOSPExtended**](https://github.com/AospExtended)
 * [**AOSiP**](https://github.com/AOSiP)
 * [**CrDroid**](https://github.com/crdroid)
 * [**Dirty Unicorns**](https://github.com/DirtyUnicorns)
 * [**LineageOS**](https://github.com/LineageOS)
 * [**ViperOS**](https://github.com/ViperOS)
