![KrakenProject](https://raw.githubusercontent.com/KrakenProject/KrakenStuff/master/img/kraken-banner-XDA.png)

Download the Source
===================

Please read the [AOSP building instructions](http://source.android.com/source/index.html) before proceeding.

Initializing Repository
-----------------------

Initiate core trees without any device/kernel/vendor:
```bash
repo init -u https://github.com/KrakenProject/manifest.git -b pie
```

Then to sync up:
```bash
repo sync -c -f -j4 --force-sync
```
***

Building
--------

After the sync is finished, please read the [instructions from the Android site](http://s.android.com/source/building.html) on
how to build.

You can also build for specific devices (eg. whyred) like this:
```bash
. build/envsetup.sh
lunch aosp_whyred-userdebug
mka bacon -j4
```
Remember to `make clobber && make clean` every now and then!
