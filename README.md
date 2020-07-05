420rom Kernel Tree for Samsung Galaxy Tab S6

Supported Models: T860 & T865

Contributors
evdenis (CruelKernel)
NZNewbie - for adding fiops scheduler
ExtremeGrief - for overall improvements, porting maple scheduler
thehacker911 - overall improvements and advices
@bamsbamx - ported boeffla_wakelock_blocker module
Nico (@NicoMax2012) - ported moro sound module
How to install
First of all, TWRP Recovery + multidisabler should be installed in all cases. It's a preliminary step. Next, backup your existing kernel. You will be able to restore it from TWRP Recovery in case of problems.

Recovery
Reboot to SHRP Recovery. Flash boot.img in boot slot.

Heimdall
Reboot to Download Mode. bash $ sudo heimdall flash --BOOT boot.img

``

### Franco Kernel Manager

Flash boot.img with FK Manager.

## Pin problem (Can't login)

The problem is not in sources. It's due to os_patch_level mismatch with you current
kernel (and/or twrp). CruelKernel uses common security patch date to be in sync with
the official twrp and samsung firmware. You can check the default os_patch_level in
build.mkbootimg.* files. However, this date can be lower than other kernels use. When
you flash a kernel with an earlier patch date on top of the previous one with a higher
date, android activates rollback protection mechanism and you face the pin problem. It's
impossible to use a "universal" os_patch_level because different users use different
custom kernels and different firmwares. CruelKernel uses the common date by default
in order to suite most of users.

How can you solve the problem? 6 different ways:
- You can restore your previous kernel and unlock problem will gone
- You can flash [backtothefuture-2099-12.zip](https://github.com/CruelKernel/backtothefuture/releases/download/v1.0/backtothefuture-2099-12.zip)
  in TWRP to set the os_patch_level date for your boot and recovery partitions to 2099-12.
  You can use other than 2099-12 date in the zip filename. You need to set it to the same
  or greater date as your previous kernel. Nemesis and Los (from ivanmeller) kernels use 2099-12.
  Max possible date is: 2127-12. It will be used if there will be no date in the zip filename.
- You can check the os_patch_level date of your previous kernel here
  https://cruelkernel.org/tools/bootimg/ and patch cruel kernel image to the same date.
  If your previous kernel is nemesis, patch cruel to 2099-12 date.
- You can reboot to TWRP, navigate to data/system and delete 3 files those names starts
  with 'lock'. Reboot. Login, set a new pin. To fix samsung account login, reinstall the app
- You can rebuild cruel kernel with os_patch_level that suites you. To do it, you need to
  add the line os_patch_level="\<your date\>" to the main.yml cruel configuration.
  See the next section if you want to rebuild the kernel.
- You can do the full wipe during cruel kernel flashing
