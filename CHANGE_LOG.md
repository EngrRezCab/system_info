CHANGES: V2.1.1
 1. Minor tweaks to revision code stuff.
 2. Added debug info during search for supplemental packages.
 3. Added preliminary detection of NVME to section 7.
 4. Added preliminary detection of PCIE to section 7.
 5. Added preliminary detection of eMMC to section 7.

CHANGES: V2.1.0
 1. Broke up fnDECODE_REV into fnGET_REVISION_CODE,
    fnNEW_STYLE_REV_CODES, and fnOLD_STYLE_REV_CODES.
 2. Additional handling of new-style warranty-void flag.
 3. Added pi model release date to top of Section 1.

CHANGES: V2.0.9
 1. Reworked pre-encoded revision code support.
 2. Show a comment with some models, when displaying
    results of the revision code exam.  Examples include
    reworked note about early 4Bs with the USB-C power design
    flaw, and a new note for Model Bs w/ fuse & D14 mods.
 3. Research suggests rev codes for the as yet unreleased CM4
    may be [abcd]03141 - comments & logic updated accordingly.
 4. Added a note in the README.md about "git pull" updates
    that fail, due to detected changes in the local copy
    conflicting with what git last knew about the files you
    last cloned/pulled.  (git reset --hard origin/master)

CHANGES: V2.0.8
 1. Formatted/aligned output of meminfo data.
 2. Support for older (pre-encoded) revision codes (Model A, etc.)
    added to fnDECODE_REV and fnPRINT_DECODED_REV

CHANGES: V2.0.7
 1. Added missing wildcard on help screen.
 2. Tweak fnCHECK_CMDLINE
 3. Added "systemd-analyze security" to Services

CHANGES: V2.0.6
 1. Added "-h" as an alternative to "--help" cmdline parameter.
 2. Added a brief header at top of fd3 debugging log.
 3. Improved the ${PATH} assignment.

CHANGES: V2.0.5
 1. Determine if fd3 has been redirected to a file.  If so, display the
    name of the debug log at the bottom of the system_info report.
 2. Help screen added, to describe supported cmdline parameters.

CHANGES: V2.0.4
 1. Modified debugging/trace logging to be available on file descriptor 3.
    Simply redirecting with "3> debug.log" on the cmdline will send
    debugging data to the specified file.  Screen ouput, and the normal
    report file remain unchanged.
 2. Added the file "DEBUGGING.md" to the github page.  This file explains
    how I chose to implement a debug/trace log, useful in testing and
    development.

CHANGES: V2.0.3
 1. Minor tweaks to the footer of the report
 2. Fixed a bug in overwriting/updating the .system_inforc file, caused
    by the addition of "set -o noclobber", in V2.0.2

CHANGES: V2.0.2
 1. Added bash ${OSTYPE} to fnOS.
 2. Tweaked fnCHECK_PERMISSIONS and fnRKHUNTER
 3. Additional traps and debugging infrastructure.
 4. Removed the explicit returns from each function.

CHANGES: V2.0.1
 1. Added check for required packages "lsb-release" and "systemd".
 2. Deleted commented lines used during Pi 400 testing.
 3. Updated README.md to include info about the 400 and CM4.
 4. Added a function and traps, for errors and debugging.
 6. Cleanups suggested by shellcheck's "-o all".
 7. Cleaned up detection of chroot'd environment.

CHANGES: V2.0.0
 1. Support for the CM4 Compute Module and new Pi 400 have been added.
 2. Output of "lsb_release -a" and "hostnamectl status" added to the
    OS Config section.
 3. Local variables now initialized when declared, and explicit returns
    added to the end of each function.
 4. Removed most of the comments at the top of the script, that are covered
    in the README.md file on the github page.

CHANGES: V1.9.9
 1. Reworked some commands containing special characters.  Much cleaner now.
 2. Fixed a bug with detection of "journaled quotas".

NOTE: The version of "shellcheck" I'd been using, from the repositories, is
old, and resulted in a number of false-positives.  If you want to compile the
latest version for yourself, see: https://github.com/koalaman/shellcheck

CHANGES: V1.9.8
 Just a code cleanup release - No functionality changes.
 1. Minor tweaks to comments throughout.
 2. Minor changes to make "beautysh" (a bash beautifier) happy.
    Between beautysh and the shellcheck linter, the code has cleaned up nicely.

Side Note: It took considerable effort in a script this large to pin down
a few sections that were tripping up beautysh - quoting where special
characters were involved, constituted all of the problems.  Beautysh tells
you when there's a problem, but doesn't tell you where! [::grr::]  Ultimately,
commenting out all the functions and renabling them one at a time between passes
pinned them down.  There's a price to pay, when you get lazy while coding.  LOL

CHANGES: V1.9.7
 1. Added decoding of revision codes for CM4 and the new P400.
 2. Reworked a few "grep | awk" pipelines to do the work in awk only, reducing
    the number of unnecessary processes forked, and pipes opened and torn down.
    More such optimizations will occur as time permits.

CHANGES: V1.9.6
 1. Additional code cleanups.
 2. Added comments to each function, indicating where the function is called from,
    and what other functions it calls.
 3. Fixed a bug when detecting mounted nfs dirs.
 4. Added "cat /etc/rpi-issue" to model information.
 5. Added comments in fnDECODE_REV() listing the revision numbers I'm aware of.
    I will need to wait until the revision # for the P400 is published or provided.
 6. Simplified check for original Pi 4B USB power design flaw.
 7. Simplified check for Pi 4B 8GB, and WiringPi.
 8. Updated decoding of revision code, for the Pi 4B (8GB) model to show installed
    RAM, and for all models to properly reflect circuit board revision number
    ("1.1" instead of "1", "1.2" instead of "2", "1.3" instead of "3", etc.)

CHANGES: V1.9.5
 1. Added listing of event signals (SIGHUP, SIGINT, etc.) to OS CONFIG section.
 2. Added a little additional info to the supplemental nspawn check.
 3. Added a missing explicit check/enumeration of apparmor package.
 4. Prevent rmmod of "configs" module if already modprobed by other than the script.
 5. Replaced shebang "#!/bin/bash" with "/usr/bin/env bash".
 6. Revised "trap" statement to use symbolic names rather than signal numbers.
 7. Reworked detection of the OVERLAY FILESYSTEM checks.
 8. Cleaned up a bunch of code as recommended by "shellcheck" static analysis tool.

CHANGES: V1.9.4
 1. A few additional variables scoped as local.
 2. Some flags set, if kernel supports features used elsewhere in the script.
 3. Changed a "[" test to "[[" that was missed in the last update.
 4. Moved modprobe/rmmod of kernel module "configs" to seperate functions.
 5. Added support for supplemental package apparmor to System Security section.

CHANGES: V1.9.3
 1. Tweak the OS version check.
 2. Added bash version to OS CONFIG section.
 3. Fixed bug in chroot'd environment detection.
 4. Fixed bug retrieving sysctl kernel variables.
 5. Added support for supplemental package "auditd" to System Security section.
 6. Added terminfo data display for user's $TERM setting.
 7. Added contents of /etc/login.def to System Security section.
 8. Mainline was really cluttered - moved several parts to functions to clean
    it up, and created fnMAIN.
 9. For coding style consistency, and to further discipline myself to
    adopt bash syntax & conventions (I'm a KSH guy), all "[" tests have been
    changed to "[[".
10. Local variables have been explicitly scoped as local.

CHANGES: V1.9.2
 1. Misc. typo's fixed.
 2. Added support for supplemental packages "lynis", "ufw", "rkhunter",
    and "unhide" to "System Security" menu option.
 3. Added "SYSTEM_INFO (X): " prefix to all section banners, to minimize
    confusion with some called tools that insert their own banners or
    section breaks into the report output.  The "X" shows the main menu
    option under which that section of the report falls.

CHANGES: V1.9.1
 1. Changed the menu layout to a two-column format.
 2. Added main menu option "System Security".
 3. Moved existing user checks, last logins and login failures, users
    currently logged in, sudoers check, permissions check, chkrootkit,
    clamav, and the nmap portscans to new "System Security" menu option.
 4. Added support for supplemental packages "tripwire" and "snort",
    to the new "System Security" menu option.

CHANGES: V1.9.0
 1. Added a check for any broken package dependencies
 2. Added strict syntax check of sudoers files
 3. Re-worked non-system user account info to add password aging info,
    homedir perms/ownership, and user's ~/.ssh dir & file perms and ownership.
 4. Added inspection of key system directory perms and ownership.
 
CHANGES: V1.8.9
 1. Check if homedir exists, when checking regular (non-system) users
 2. Added last logins & failures, and who is currently logged in.

CHANGES: V1.8.8
 1. Added check to see if kernel supports auditd.
 2. Added inspection of regular (non-system) user accounts...
    Listing homedir, shell, numeric UID
    Which groups the account belongs to
    Whether the account has a null passwd field (a bad thing)
    Whether the account has an initial password set
    Whether the account has a password, but is administratively locked

CHANGES: V1.8.7
 1. Improvements to clamav-related info.
 2. Added clamav to the list of supplemental packages listed in README.md
    and in the comments at the top of the script, forgotten in the last release.
 3. Renamed function fnLOCAL to fnLOCALE
 4. Cleaned up a number of compound "grep" pipelines.
 5. Added display of any overclock-related settings present in config.txt.
    Note: This does NOT take into account any "conditional branching"
    stanzas ( ie: "[pi4]", "[all]", etc.) that may be present in the config.txt.

CHANGES: V1.8.6
 1. Improved check for supported os version.
 2. Added supplemental check for clamav...
    Shows clamscan, clamd, and freshclam versions, and systemctl status.

CHANGES: V1.8.5
 1. Added detection of apparmor-enabled kernel

CHANGES: V1.8.4
 1. Fixed a bug with cmdline parameter
 2. Updated README.md to include mention of the cmdline

CHANGES: V1.8.3
 1. Added a way to force a specific module during development/testing.

    Though not originally intended for general use, this allows for specifying
    a single main menu option via the cmdline.  Just pass the main menu
    option number as a cmdline parameter.  Examples would include:
      system_info 1
      system_info 2
      system_info 3
      ...and so on.
    The use of a cmdline parameter ignores whatever is saved in the user's
    ${HOME}/.system_inforc file.

    ONLY A SINGLE MAIN MENU OPTION NUMBER CAN BE SPECIFIED.  However, if you specify
    option 16 ("system_info 16"), ALL main menu options will be executed, just as
    when that option is chosen via the menu.

 2. Added an alert bell when the script is aborted.
 3. At end of report, indicate if no menu options were selected.
 4. Improved the visibility of main menu selected option indicators, by user request.

CHANGES: V1.8.2
 1. Fixed bug determining whether to rmmod "configs" module.
 2. Show systemd default.target (graphical, multi-user, etc) in OS Config section.
 3. Show configured GUI and console autologin ID's in OS Config section. 

CHANGES: V1.8.1
 1. Added check for "ID=raspbian" in /etc/os-release
 2. If we modprobe the "configs" module, rmmod it when done with it.
 3. In prereqs, display "sudo is available" status only if run by non-root user.
 4. Minor reorg of some code.
 5. Reworded instructions on the main menu based on feedback from a user.

CHANGES: V1.8.0
 1. A few minor cosmetic tweaks
 2. Added support for supplemental package "chkrootkit"

CHANGES: V1.7.9
 1. When searching for installed supplemental packages, some packages have different names
    between Stretch and Buster - Stretch has "pigpio" to Buster's "pigpiod", and Stretch has
    "docker.io" to Buster's "docker-ce-cli".  Added a fix to vary the searched-for
    supplemental package names, based on whether the release is Stretch or Buster.
 2. Disable "vcgencmd display_power" tests on Stretch, as the command does not support the
    "-1" flag which specifies which display to check.
 3. Added support for a touch file, if the user wants to run the sysbench fileio tests
    (assuming they have sysbench installed.) - manually "touch ${HOME}/.system_info_io" to
    enable that test, "rm ${HOME}/.system_info_io" (if it exists), to prevent that test's
    execution.  IMPORTANT: This test creates, writes, reads and deletes 128 files, 16Mb each
    (2GB total).  Most people will NOT want to do that much writing to their media (particularly
    those running on SD cards and SSD drives.)  Hence, the default behavior is not to run the
    I/O test unless the user deliberately creates the touch file.  Note too, that this test adds
    5 additional minutes to the script's total execution time.

CHANGES: V1.7.8
 1. sort MAC-ADDRESS(ES)
 2. run supplemental ethtool against additional network interfaces
 3. don't bother with "systemctl status logrotate.timer" on Stretch
 4. Fixed missing ${DEV} variable in fnSMART function
 5. Replaced fstrim "-A" flag with "--all", and removed "-n" flag, for Stretch compatibility
 6. Added missing sudo to an fstrim command
 7. fstrim now contingent on existence of udev rules
 8. add supplemental package lm-sensors

CHANGES: V1.7.7
 1. Fix docker info on Stretch
 2. Added "machinectl list" and misc. fixes to nspawn section

CHANGES: V1.7.6
 1. Added supplemental conversion to Fahrenheit, to ring oscillator stats.
 2. Added check of SELINUX support as "m", in addition to "y", in kernel config
 3. Don't attempt hdparm if not installed.

CHANGES: V1.7.5
 1. Added a "noatime" check of /etc/fstab to the SMART section - SSD-hosted filesystems
    should use the "noatime" attribute to improve device lifespan.
 2. Renamed SMART section to USB ATA/SATA & SCSI/SAS STORAGE WITH SMART TECHNOLOGY (***)
 3. Added Contents of /etc/containerd/config.toml to DOCKER section
 4. Misc. updates to some comments.
 5. Added detection of SELINUX-capable user-compiled custom kernel.
 6. Small hack to force all menu selections during testing.

CHANGES: V1.7.4
 1. Reworked SMART data to provide more info / greater detail.

CHANGES: V1.7.3
 1. Added requirement for package initramfs-tools
 2. Added OVERLAY FILESYSTEM section, with detection of ro /boot

CHANGES: V1.7.2
 1. Added "SYSCTL KERNEL VARIABLES" section to the OS Config block (Menu option 3)
 2. Cleaned up hdparm output.
 3. Detect either an undefined, or "dumb" ${TERM}, in fnROW_COLS
 3. Eliminate unnecessary 'cat' from fnLOGROTATE
 4. Added USB "quirks" check

CHANGES: V1.7.1
 1. Added missing sudo, and other changes to crontabs section.
 2. Added some "if exists" tests before cat-ing allow/deny files.

CHANGES: V1.7.0
 1. Move fnTITLE from fnPRELIM and fnACTIONS, to mainline.
 2. Added fnREPORT_ACTIONS to the top of  the report, in addition to the bottom.
 3. Initialize report so that all use of "tee" is append mode.
 4. Added "cron" as required package, and "at" as supplemental package.
 5. Added "JOB SCHEDULING - CRON" section to OS Config
 6. Added "JOB SCHEDULING - AT (***)" section to OS Config (Menu option 3)
 7. Added "LOGROTATE" section to Logging (Menu option 5)

CHANGES: V1.6.9
 1. renamed "RC.LOCAL" banner to "CONTENTS OF RC.LOCAL" to reduce confusion.
 2. fix 1-wire function "fnW1"/"fn1W" typo.

CHANGES: V1.6.8
 1. Added a notation in the summary that menu option 16 overrides any/all other selections
    that may have been made.
 2. Added output of "ls -1 /sys/bus/w1/devices" to fnW1, by request.

CHANGES: V1.6.7
 1. Added checks during initialization to ensure not running in a VM or chroot'd environment.
 2. Added supplemental package "systemd-container".
 3. Added NSPAWN (***) section / checks for nspawn-related virtual environments to
    main menu option 14 (Containers & Virtualization)

CHANGES: V1.6.6
 1. Moved RING OSCILLATOR STATS to it's own function, in fnGROUP_PERFORMANCE.
 2. Added section headings to the output, to indicate which sections of the
    report corresponded to which main menu selections.

CHANGES: V1.6.5
 1. With WiringPi deprecated, prevent use of WiringPi on the new Pi 4B 8GB model.
    Pi 4B 1/2/4GB models will still be examined, if WiringPi 2.5.2 is installed.

CHANGES: V1.6.4
 1. Added shared memory, message and semaphore details to IPC STATUS section

CHANGES: V1.6.3
 1. Added HDPARM SATA/IDE DEVICE PARAMETERS section
 2. Added hdparm as additional supplemental package
 3. Broke out 'lshw -businfo' to create tmpfile right after supplemental package
    check, and not delete the tmp file it creates until the end of the script,
    so that the info it gathers would be available to other modules that depend
    on that info.  Before breaking the script up with the menu, the info was
    available all throughout the script.  Once the menu broke things up, it was
    possible that sections chosen in the menu would not have the info available,
    since the function that gathered the info wouldn't be run.  New setup ensures
    the info is gathered (and preserved) before any menu selections are made.

CHANGES: V1.6.2
 1. Added VIDEO CORE VERSION AND LOG STATUS section
 2. Added VIDEO CORE OUT-OF-MEMORY EVENTS section
 3. Added VIDEO CORE RELOCATABLE MEMORY STATS section
 4. Added RING OSCILLATOR STATS section
 5. Added DISPLAY POWER UP STATUS section
 6. Fixed missing HDMI info not displayed menu option 1 or 16 hadn't been selected (display driver would be undefined) 

CHANGES: V1.6.1
 1. Swapped options 14 & 15 on the menu, to put docker ahead of package list
 2. changed package dependency from docker-ce to docker-ce-cli
 3. Added "sed 's/\r//'" to the writing of the report, to eliminate risk of DOS CR's creeping into the report.
 4. Added "2>/dev/null" to a number of "cat" and "grep" commands
 5. Updated the required and supplemental package lists in the opening comments
 6. Minor tweaks to supplemental notationsda

CHANGES: V1.6.0
 1. Added menu option for "Containers & Virtualization"
 2. Added support for DOCKER

CHANGES: V1.5.9
 1. Added LIRC - LINUX INFRA-RED COMMUNICATION DEVICES section.
 2. Added lirc as supplemental package.

CHANGES: V1.5.8
 1. Fixed a broken "grep -v" in UARTS AND USB SERIAL PORTS
 2. Added "raspi-gpio get" data to each additional Pi 4 uart configured
 3. Added a way to prevent the user from trying to run the script under
    any shell other than bash (for example: "sh scriptname", or "ksh scriptname")
 4. Added procps as a required package
 5. Gathers some info on the Pi 4B's additional I2C busses.

CHANGES: V1.5.7
 1. Added hciconfig output to BLUETOOTH CONTROLLERS section
 2. Added "dtoverlay -h" details about 4B uarts to UARTS AND USB SERIAL PORTS section
 3. Added saving & recalling the last menu items selected, and pre-loading the menu
    with those saved selections, the next time the script is run.

CHANGES: V1.5.6
 1. Added a summary to the bottom of the report, listing which menu selections were
    made to generate the report,
 2. Increased number of serial port devices to look for, from 0 thru 1, to 0 thru 5 (to allow for 4B's four additional uarts)
 3. Reworked UARTS AND USB SERIAL PORTS section

CHANGES: V1.5.5
 1. Clear the screen at beginning of the script.
 2. Added CHECKING REPOSITORIES section to check the repositories for available upgrades
 3. Added CONFIGURED REPOSITORIES section to list configured binary and source repos
 4. Added total time to execute, at the end of the report
 5. Simplified "if files exist" in fnLOCALE
 6. Fixed the Pi4B's 2711 voltages to display like the others.
 7. Ran "shellcheck" against the script, and cleaned up a few coding malpractices it found.
 8. Fixed typo in RSYSLOG.CONF section.
 9. Added an elapsed time to execute, to the footer of the report.

CHANGES: V1.5.4
 1. Replaced degree symbol (°) with $'\xc2\xb0' construct - was causing UTF-8 Unicode rather than ASCII text, confusing github.
 2. Removed unused section CONFIG.TXT VALUES ABOVE, THAT ARE "LIVE"
 3. Set every module as a function, to facilitate rearranging order and prepping for a menu of some sort.
 4. Added CURRENT ROWS & COLUMNS section
 5. Created menu system, and all report data is now writtien to a report file in the user's homedir

CHANGES: V1.5.3
 1. Added USB STORAGE WITH TRIM ENABLED section
 2. Added detection of KVM-enabled kernel
 3. Added supplemental package "smartmontools"
 4. Added supplemental USB STORAGE WITH S.M.A.R.T. (***) section

CHANGES: V1.5.2
 1. Added supplemental OPERATING SYSTEM ERROR NUMBERS (***) section
 2. Updated required and supplemental package lists in the comments at top of the script
 3. Added supplemental package "sysbench"
 4. Added supplemental SYSBENCH CPU BENCHMARK (***) section
 5. Added supplemental SYSBENCH MEMORY READ/WRITE BENCHMARK (***) section
 6. Added (but commented out) supplemental SYSBENCH FILEIO BENCHMARK (***) section

CHANGES: V1.5.1
 1. Marked ULIMIT AND COREDUMPS as supplemental "(***)"
 2. Greatly simplified PI MODEL 4B EEPROM CONFIG.  I will no longer document
    each setting here, instead referring the user to online documentation:
    https://www.raspberrypi.org/documentation/hardware/raspberrypi/bcm2711_bootloader_config.md
 3. Added DMESG - WARN and DMESG - FAIL sections
 4. Minor tweaks to HDMI Display detection
 5. Added LED TRIGGERS section
 6. Added LOADED OVERLAYS section
 7. Added LOADED DTPARAMS section

CHANGES: V1.5.0
 1. Updated comments at top of script to reflect recent additional packages.
 2. Modified fnBANNER to help visually divide modules.
 3. Added fnSUB_BANNER to help visually divide sections of a single module.
 4. Added a title screen
 5. Added m4 and perl-base as supplemental packages
 6. Merged in "syslogconf" perl logic to create RSYSLOG.CONF ANALYSIS (***)

CHANGES: V1.4.9
 1. Added sed as a required package
 2. Added mdadm as a supplemental package
 3. Added lvm2 as a supplemental package
 4. Added RAID ARRAY CONFIGURATION (***)
 5. Added LOGICAL VOLUME MANAGER CONFIGURATION (***)

CHANGES: V1.4.8
 1. Refinements to core dump reporting
 2. Added QUOTAS section

CHANGES: V1.4.7
 1. Added "systemctl list-jobs" to SYSTEMD-ANALYZE CRITICAL-CHAIN
 2. Modified SCALING GOVERNOR to consider settings other than just "ondemand".
 3. Added "systemctl list-jobs" to SYSTEMD-ANALYZE CRITICAL-CHAIN
 4. Minor reformatting of CLOCK FREQUENCIES and VOLTAGES
 5. Added ULIMIT AND COREDUMPS section
 6. Added systemd-coredump as a supplemental package

CHANGES: V1.4.6
 1. Added "vcgencmd dispmanx_list" to HDMI DISPLAY DATA
 2. Tweaked HDMI DISPLAY DATA to better visually seperate HDMI 0 results from HDMI 1 results.
 3. Added I2S, I2C, and SPI module checks, and added additional info to 1-WIRE check.
 4. Added blkid info to DISK CONFIGURATION section

CHANGES: V1.4.5
 1. Fixed stderr redirect with xrandr
 2. Added detection if w1-gpio devices
 3. Added ${SUDO} to PI MODEL 4B EEPROM UPDATE STATUS

CHANGES: V1.4.4
 1. Use "vcgencmd get_config arm_64bit" instead of uname to determine 32 or 64-bit kernel
 2. Added camera led status
 3. Added x11-xserver-utils as an optional package
 4. Added CURRENT X-DISPLAY RESOLUTION (***) section
 5. Added optional package rng-tools
 6. Added HARDWARE RANDOM NUMBER GENERATOR (***) section

CHANGES: V1.4.3
 1. Added confirmation of /var/log/journal owner/group/perms
 2. Disabled HDMI DISPLAY DATA and CURRENT SCREEN RESOLUTION sections if vc4-kms-v3d(-pi4) display driver
 3. Re-worked VIDEO4LINUX DEVICES

CHANGES: V1.4.2
 1. Fixed typo, added perms check, sync, flush, journal sizes, list-boots, and disk-usage to PERSISTENT JOURNALING
 2. Fixed error in GPU temp formatting
 3. Moved OPERATING SYSTEM closer to the top

CHANGES: V1.4.1
 1. Minor cleanups
 2. Added simple check, for 64-bit or 32-bit kernel, to OPERATING SYSTEM section

CHANGES: V1.4.0
 1. Disabled display of I2CDETECT section if "dtparam=i2c_arm=on" not found in config.txt
 2. Disabled output of BLUETOOTH DEVICES section if no paired devices are found
 3. For "tvservice --modes=${TVGROUP}" in HDMI DISPLAY DATA section, force the group
    to DMT if display "group" is neither "DMT" nor "CEA", but "CUSTOM"
 4. Reworked the search for supplemental packages, similar to the search for required packages
 5. Added comments about minimum memory required for camera and HW codecs, to the MEMORY SPLIT section
 6. Re-added "bc" as a required package.
 7. Renamed Core Temp to GPU Temp, and added ARM Temp, to TEMPERATURES section.
 8. minor tweaks to formatting of temperatures

CHANGES: V1.3.9
 1. Fixed 4B identifying wiringpi less than 2.52 as an installed supplemental package
 2. Fixed problem with wiringpi non-2.52 mistakenly running "gpio readall" test on 4B
 3. Fixed display of missing parameters in PI MODEL 4B EEPROM CONFIG

CHANGES: V1.3.8
 1. Added missing "net-tools" as being a required package
 2. Added "NETSTAT" section
 3. Added additional 4B clock frequencies to CLOCK FREQUENCIES section
 4. Added 4B-specific voltages to VOLTAGES section
 5. Added 4B-specific clocks to CLOCK FREQUENCIES section

CHANGES: V1.3.7
 1. Added confirmation of playback and capture devices before attempting to display,
    to the ALSA PLAYBACK AND CAPTURE DEVICES section.
 2. tidy up stderr from lshw throughout.
 3. Split off current screen resolution to it's own CURRENT SCREEN RESOLUTION section
 4. Added notes to the HARDWARE-ACCELERATED CODECS section
 5. Added MAC-ADDRESS(ES) section
 6. Re-ordered the PI 4B EEPROM sections and split out PI MODEL 4B EEPROM UPDATE STATUS
 7. Added package rpi-eeprom as a required package, but only if the Pi is a 4B.
 8. Added a detailed breakdown of the 4B's EEPROM config

CHANGES: V1.3.6
 1. Moved DECODED SYSTEM REVISION NUMBER section to right after PRELIMINARY CHECKS.
    Also preserved each decoded value in appropriate variables that
    can be referenced to make decisions easier, later in the script.
 2. Added check of wiringpi version number if a Pi 4B, in the search for supplemental packages
 3. Added contents of rc.local

CHANGES: V1.3.5
 1. Updated comments in a few places.
 2. Added logic to DECODED SYSTEM REVISION NUMBER section, to
    call attention to early 4B's with USB-C power design flaw.
 3. removed unnecessary "type -path" test from SCALING GOVERNOR
 4. Added supplemental package ethtool, along with ETHTOOL (***) section.
 5. Added "| tee /dev/null" to several systemctl statements, and to
    "dpkg -l", to keep from paging/pausing output.
 6. Demoted wiringpi from required to supplemental package, due
    to it's deprication, and the Pi 4B.

CHANGES: V1.3.4
 1. renamed codecs section to "gpu hardware-accelerated codecs"
 2. Added note that "gpu_mem=16" disables codecs, and "gpu_mem=96"
    is minumum for codecs to run.
 3. Added v4l-utils as a required package
 4. Added "V4L2-CTL CODECS" section w/ notes about H265 on Pi 4B
 5. Added ADDITIONAL VIDEO4LINUX DEVICE section to loop through
    "v4l2-ctl -d ${NUM} --all", for other than the onboard
    video10, video11, video12 (decode, encode, resize/convert)
 6. Added supplemental package rtl-sdr
 7. Added RTL-SDR TUNER section

CHANGES: V1.3.3
 1. Corrected "type -path" bug with "mounted nfs dirs"
 2. Reworked the hardware codecs.  No hardware decoding of MPG2 and WVC1 on the Pi 4B.
 3. Added a few checks to ensure files exist before reading them.
 4. Fixed search for on-hold packages.

CHANGES: V1.3.2
 1. Minor comment and organizational changes
 2. Added check for packages marked as on "hold"
 3. Added supplimental package python3-gpiozero
 4. Added SYSTEM DIAGRAM section using "pinout"
 5. Added required package "coreutils"
 6. Changed "dc" from a required to supplemental package dependency
 7. Removed "bc" as a dependency - using bash for integer math instead
 8. Tweaked memory split and processor speeds to use printf

CHANGES: V1.3.1
 1. Added supplemental package sysstat, for mpstat and iostat
 2. Added nfsiostat (if remote nfs shares are mounted)
 3. Added Broadcom watchdog timer
 4. Added missing required package iproute2 as required package
 5. Removed most of the redundant "type -path" tests.
 6. Removed "fnREQUIRE".

CHANGES: V1.3.0
 1. Added /etc/hosts.deny and /etc/hosts.allow
 2. Added portmapper rpcinfo
 3. Added exported nfs dirs
 4. Added mounted nfs dirs
 5. Added smbstatus
 6. Added mounted cifs dirs
 7. Improved the checks for supplemental packages
 8. Added confirmation of Pi2B v1.2 to OTP boot from usb check

CHANGES: V1.2.9
 1. Added Pi4 EEPROM Version, and EEPROM Config
 2. Added Pi4 EEPROM upgrade required check
 3. OTP boot mode now only checked for non-Pi4 models
 4. Added check of the dmesg ring buffer to ensure data
    we expect to retrieve hasn't been overwritten
 5. Added lshw generic class
 6. Added lshw input class
 7. Added meminfo display

CHANGES: V1.2.8
 1. Added github URL
 2. Fixed nmap routine to not enforce that it be installed
 3. Re-worked list modules to not require a tmpfile
 4. Added uname to commands passed to fnREQUIRE
 5. Fixed wpa_supplicant display password concealment
 6. "2>/dev/null" added to amixer, aplay, and arecord
 7. Added "systemd-analyze time" and "systemd-analyze critical-chain"
 8. Added "systemd-analyze blame"
 9. Added "systemctl status"

CHANGES: V1.2.7
 1. Added localization settings - language, keyboard, timezone
 2. Activated the loaded modules section, and updated the comments
 3. Activated the installed package list section, and updated the comments
 4. Added announcement that lpstat and nmap are found to be installed
 5. Added detection of Official 7" Touchscreen

CHANGES: V1.2.6
 1. updates to various comments
 2. fixed an erroneous error msg with calls to "dpkg -l"
 3. added a couple missing calls to sudo
 4. added IPv6-specific handling for route table display and port scanning

CHANGES: V1.2.5
 1. Added "SCANNING FOR" to the nmap port scan, to explain the delay.
 2. Added "systemctl list-unit-files"
 3. Added "uptime -p" to the OPERATING SYSTEM section
 4. Added wpa_supplicant file, with concealment of stored passwords
 5. Added a trailing newline to fnBANNER to give data breathing room
 6. Fixed a couple my missing sudos with "lshw -class"

CHANGES: V1.2.4
 1. Not a requirement/dependency, but if it is installed, the script
    will perform a port-scan of all network interfaces with an ip
    address, using "nmap".
 2. list all installed modules
 3. list all installed packages

CHANGES: V1.2.3
 1. Fixed determining which OpenGL driver (Full or Fake) is running
 2. Corrects an error in a dependency check
 3. Small fix to ip neighbors.

CHANGES: V1.2.2
 1. Corrected a "||" for "&&" error in a dependency check
 2. Small fix to ip neighbors 

CHANGES: V1.2.1
 1. Added "lpstat -t" printer status
 2. Added "ip neigh" (arp cache)
 3. Added visible WiFi access points
 4. Added report date/time to report
 5. Tweaked determination of active loaded video driver.
    This still needs work, as conditional branching in config.txt
    could present issues if multiple driver references appear
    in the config.txt file.
 6. Minor wording tweaks here and there
 7. Added display of /etc/hosts, resolv.conf, and networks files
 8. Display /etc/iptables.up.rules and /etc/ip6tables.up.rules
 9. Show contents of /etc/fstab
10. check cmdline.txt for "ipv6.disable=1"
11. Added cpu information (lscpu)
12. expanded the storage device info section
13. Re-ordered the sections a bit

CHANGES: V1.2.0
 1. Added some details for any found /dev/tty/ACM* devices
 2. Added some details for any network adaptor hardware
 3. Added some details for any multimedia devices
 4. Added some details for any storage devices
 5. Added detection of camera
 6. Checking additional codecs
 7. Decode Processor Throttling Status
 8. Check OTP for boot-from-usb.

CHANGES, ROUND 4:
 1. Added decoding of the system's revision number to show Manufacturer, Warranty status, etc.
 2. When checking dependencies, I added an exception for the "wiringpi" package.  Some prefer
building the latest libraries from source, instead.  If the package check fails, yet the "gpio"
tool built from the source tarball is found in the user's $PATH, we allow that alternate version.
 3. Added minimum OS version check (Stretch or later required.)

CHANGES, ROUND 3:
 1. Added hostname, and cleaned up display of serial number.
 2. Renamed "Speed Governor" to "Scaling Governor", to reflect what its called in all the docs.
 3. Query dpkg directly, to see if each required package is installed.
 4. Expanded the HDMI DISPLAY information block to add more data.
 5. Show which video driver is loaded: Open GL, "Fake" Open GL, or the Default Broadcom driver.
 6. Took a stab at reporting on BOTH HDMI ports of a Pi 4B.  Guessing at this, as I dont own a Pi 4B.

CHANGES, ROUND 2:
 1. Fixed "MEMORY SPLIT" reporting in a way that accurately works with Pi 4 > 1GB, and removed the
    "Total memory" (free) work-around, as it didn't really convey the intended information.
 2. Added the "if type -path" test, to some recently added stanzas.
 3. Added the Pi's Serial Number.
 4. Added "gpio readall" (requires that the wiringpi package be installed).
 5. Renamed the "banner" function to "fnBANNER", since "banner" is the name of an unrelated
    and legitimate "banner" command that has been part of Unix for 40+ years.
 6. Also renamed "require_util" to "fnREQUIRE".  (See comments on my personal coding style, below)
 6. Ran the script through a beautifier, to make the code formatting consistent.
 7. Did away with the "fail" function, and reworked the test for the sudo command.
    I can't see *any* interactive user account not having /bin and /usr/bin in their path,
    nor have I ever seen a *nix variant put the sudo command anywhere outside the user's path.
    Rather than explicitly test for the sudo binary file in multiple dirs, I changed this to
    use "type -path sudo", to set ${SUDO}.  This might also warrant reducing the list of commands
    searched for when calling fnREQUIRED.  (Do we *really* need to check for commands like
    "cat", "ls", and so on?)  I'd focus only on commands from the supplemental packages, and skip
    those that are part and parcel of every raspbian bare-metal install.

CHANGES, ROUND 1:
 1. Incorporated William's changes.
 2. Fixed bluetoothctl commands to work with Stretch.
 3. Removed wlan0-only restriction from netstat.  All interfaces are now displayed.
 4. Added "2>&1" to i2cdetect to capture warnings about busses that don't support detection commands.
 5. Added HDMI current display mode (tvservice -s)
 6. Added operating system version info.  This includes dotting-in the /etc/os-release file.
 7. Added filesystem type to "df -h" - now "df -h -T", in disk configuration section.
 8. Added "PATH=${PATH}:/sbin:/usr/sbin" because some tools not necessarily needing root access
    to execute were being flagged as a "Missing utility", when in fact, they are installed, but
    not in the user's $PATH.
 9. Added "hwclock" to RTC section, to show hardware time in addition to OS "date" command.
10. Relaced "netstat -r" with route
