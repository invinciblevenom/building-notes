# Compile LineageOS

**Initial phase: install git and repo tools**

0. Check for updates

        sudo apt-get update && sudo apt-get upgrade

1. Install required packages.

        sudo apt-get install android-tools-adb android-tools-fastboot git-core gnupg flex bison gperf build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev libgl1-mesa-dev libxml2-utils xsltproc unzip python megatools

2. Make a directory to place repo tool.

        mkdir ~/bin

3. Set path to use repo tool

        PATH=~/bin:$PATH

4. Downoad the repo tool.

        curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo

5. Make the tool executable.

        chmod a+x ~/bin/repo

**Second phase: Set Environment**

6. Install required packages for Android/Lineage development.

        sudo apt-get install bc bison build-essential ccache curl flex g++-multilib gcc-multilib git gnupg gperf imagemagick lib32ncurses5-dev lib32readline6-dev lib32z1-dev liblz4-tool libncurses5-dev libsdl1.2-dev libssl-dev libwxgtk3.0-dev libxml2 libxml2-utils lzop pngcrush rsync schedtool squashfs-tools xsltproc zip zlib1g-dev

7. Make a working directory 

        mkdir lineage

8. Switch to working directory.

        cd lineage

9. Input Git username

        git config --global user.name "Ansh Singh"

10. Input Git Email

        git config --global user.email "anshsingh.14.lko@gmail.com"

11. Initialise repo.

        repo init -u git://github.com/LineageOS/android.git -b lineage-17.1

12. Use nproc command to know no. of CPUs you have

        nproc (get "n" from here)

13. Use the above ```nproc``` vaue to sync source code

        repo sync -c -j8 --force-sync --no-clone-bundle --no-tags

**Third phase: Setting ccache and Jack**

__a. ccache in Android 9 and below__

14. Use CCACHE. If you want to use Ccache then execute below 3 commands.

        export USE_CCACHE=1

15. Configure how much drive space ccache can use

        prebuilts/misc/linux-x86/ccache/ccache -M 50G
        
        export CCACHE_COMPRESS=1
        
__b. ccache in Android 10 and above__

        export USE_CCACHE=1; export USE_CCACHE_EXEC=$(command -v ccache); ccache -M 50G;
        
 where 50G is the space allocated to cache.
        
16. Setup Jack

        export ANDROID_JACK_VM_ARGS="-Xmx16g -Dfile.encoding=UTF-8 -XX:+TieredCompilation"
        
Remember to replace 16 in -Xmx16g with atleast half of your RAM. Eg: If I have 16GB RAM then it is -Xmx8g.

**Fourth phase: Start compiling**

17. Start build

        . build/envsetup.sh

18. Compile (This depends upon the ROM, do check once)

        brunch ROMName_codename_BuildVariant  -j(nproc)
        
**For Android 11** 

        m otapackage
        
**Fifth phase: Uploading to Mega (through terminal)**

19. Use below command to upload file.
        
        megaput <file> -u <username> -p <password>
