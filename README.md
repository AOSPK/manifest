The Kraken Project
===========

<a href="https://aospk.org"><img alt="SourceForge" src="https://img.shields.io/sourceforge/dm/aospk?label=KRAKEN%20DOWNLOADS&style=for-the-badge"></a>
<a href="https://www.buymeacoffee.com/mamutal91"><img alt="BuyMeACoffee" src="https://img.shields.io/badge/Buy%20Me%20a%20Coffee-ffdd00?style=for-the-badge&logo=buy-me-a-coffee&logoColor=black" /></a>

### How to apply?
- Do you want to be part of our team? Read our [**documentation**](https://github.com/AOSPK/official_devices/blob/master/README.md) and fill out our [**application form**](https://github.com/AOSPK/official_devices/issues/new/choose)

### Requirements
- Around 250G disk space
- 20G or more usable internet
- A computer with at least 16G RAM running Linux or MacOS

### Instructions
- Preparing the SERVER
    1. To prepare your server, i recommend using [**Akhil Narang**](https://github.com/akhilnarang/scripts) scripts.
    2. Make directory for the repo binary
        ```
        mkdir ~/bin
        ```
    3. Add directory for the repo binary to its path
        ```
        PATH=~/bin:$PATH
        ```
    4. Downloading repo binary and placing it in the proper directory
        ```
        curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
        ```
    5. Giving the repo binary the proper permissions
        ```
        chmod a+x ~/bin/repo
        ```
    6. Creating directory for where the ROM repo will be stored and synced
        ```
        mkdir ~/AOSPK
        cd ~/AOSPK
        ```

- Preparing the ROM
    1. Make sure you have a build environment setup.
    2. Make a new directory, cd to it and run
        ```
        repo init -u https://github.com/AOSPK/manifest -b eleven
        ```
    3. Sync!
        ```
        repo sync -c -j$(nproc --all) --no-clone-bundle --no-tags --force-sync
        ```

- Preparing device
    1. Clone your tree repositories
        Example:
          ```
          git clone https://github.com/YourUser/device_xiaomi_beryllium -b eleven device/xiaomi/beryllium
          ```
    2. Move/copy your `<ROM>.mk` (Example: `lineage.mk` or `lineage_beryllium.mk`) file to `aosp_beryllium.mk`.
    3. Open this file and
        - Set PRODUCT_NAME to `aosp_<device>` (Example: `aosp_beryllium`)
        - For a Phone or tablet with a SIM Card, add
            ```
            # Inherit from aosp vendor
            $(call inherit-product, vendor/aosp/config/common_full_phone.mk)
            ```
        - For a WiFi-only tablet, add
            ```
            # Inherit from aosp vendor
            $(call inherit-product, vendor/aosp/config/common_full_tablet_wifionly.mk)
            ```
    4. Save and exit

- Building
    1. If you want to do it manually, run:
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
- For common porting related errors, visit [**Android Building Help**](https://t.me/AndroidBuildersHelp)
- Make sure you provide relevant logs, screenshots and details with all sources you used.
