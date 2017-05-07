# Patches to enable 15KHz video output in linux
These patches allow you to enable 15KHz video output during boot process.


### Using the patches
* Clone the tag according to your kernel version
* Apply patches to your kernel sources
* Compile and install the patched kernel
* Add `video=VGA-1:640x480ec` or `video=VGA-1:800x600ez` to your bootloader, where
  * `VGA-1` is the connector name (see the kernel documentation for more info)
  * `640x480`/`800x600` is the resolution you want to force
  * `e` is needed to enable the connector (again, see the kernel documentation for more info)
  * `c`/`z` is needed to force respectively 15KHz/25KHz
* Reboot


### Using a custom EDID
* Clone the repository
* Ensure your kernel has been built with `CONFIG_DRM_LOAD_EDID_FIRMWARE` option enabled
* Copy the "[edid](edid)" directory to `/lib/firmware`
* Add `video=VGA-1:e drm_kms_helper.edid_firmware=VGA-1:edid/_EDID_NAME_` to your bootloader, where
  * `video=VGA-1:e` is needed to enable the connector
  * `drm_kms_helper.edid_firmware=VGA-1:edid/_EDID_NAME_` is needed to force the custom EDID on the connector
* Reboot

NOTES:

1. If you are doing early KMS, you must include the custom EDID file in the initramfs, or you will run into problems
2. An advantage of using custom EDID is that you can start an X server without any configuration file (AKA: without specifying a modeline as custom resolution)
3. Currently there isn't a custom EDID for 25KHz, though isn't too difficult to build one
