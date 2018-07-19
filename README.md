# kbuildparser

A standalone version of `minigolem` from the [undertaker](https://vamos.informatik.uni-erlangen.de/trac/undertaker) tool suite

## How to use it?

```
$> ./kbuildparser -h
usage: kbuildparser [-h] [-v] [-q] [-a ARCH] [directory [directory ...]]

Parser for Kbuild files

positional arguments:
  directory             input directories containing Kbuild/Makefiles

optional arguments:
  -h, --help            show this help message and exit
  -v, --verbose         increase the log level (can be specified multiple
                        times)
  -q                    decrease the log level
  -a ARCH, --arch ARCH  target architecture
```

Run the main Python script `kbuildparser` from the root of a Linux tree.

If no explicit directories are specified, the tool will walk through all Kbuild
Makefiles for the target architecture. If no architecture is specified on the
command line, it will default to `x86`.

The output will contain a mapping of files to a propositional formula with the
Kconfig options required to build them.

## Example output

```
init/calibrate.c <- CONFIG_GENERIC_CALIBRATE_DELAY
init/do_mounts.c
init/do_mounts_initrd.c <- CONFIG_BLK_DEV_INITRD
init/do_mounts_md.c <- CONFIG_BLK_DEV_MD
init/do_mounts_rd.c <- CONFIG_BLK_DEV_RAM
init/init_task.c
init/initramfs.c <- CONFIG_BLK_DEV_INITRD && CONFIG_BLK_DEV_INITRD
init/main.c
init/noinitramfs.c <- !CONFIG_BLK_DEV_INITRD
init/version.c
drivers/nvme/target/admin-cmd.c <- CONFIG_NVME_TARGET
drivers/nvme/target/configfs.c <- CONFIG_NVME_TARGET
...
```
