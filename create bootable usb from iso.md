# Create bootable USB from iso file

## Mac
    Prepare the image
        Create .img file from a .iso
        hdiutil convert -format UDRW -o /path/to/target.img /path/to/source.iso
        Rename .img.dmg to . img
        mv /path/to/target.img.dmg /path/to/target.img
    Create the bootable usb key
        diskutil list
        diskutil unmountDisk /dev/diskN
        sudo dd if=/path/to/downloaded.img of=/dev/rdiskN bs=1m
        diskutil eject /dev/diskN

## Windows
    diskpart
    list disk
    select disk n
    clean
    create part pri
    select part 1
    format fs=ntfs quick
    active
    exit
    copy iso content (unzip using 7zip)
