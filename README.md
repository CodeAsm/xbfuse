# xbfuse - Use FUSE To Mount (Original) Xbox and Xbox 360 DVD Filesystems

**Note (February, 2018):** The original build instructions below were written circa 2006 and are a bit obsolete. This source code should still compile and run on modern Linux kernels using this process:

1. Be sure to have FUSE libraries installed (as of Ubuntu 16.04, this package is 'libfuse-dev')
2. Clone this repository
3. Execute the following build command:
 
 ```gcc -D_FILE_OFFSET_BITS=64 -Wall src/main.c src/tree.c src/xdvdfs.c -o xbfuse -lfuse```

This will build the binary executable ```xbfs```. Use the *Usage* section below for instructions on running this utility.

---

xbfuse is a program that allows you to mount the filesystem of a 
Microsoft Xbox or Xbox 360 DVD as a read-only part of the Linux 
filesystem. This allows the user to browse the directory structure and 
read the files within. 

xbfuse is made possible with Filesystem in Userspace (FUSE), available 
at:

  http://fuse.sourceforge.net/

Note that it is not usually possible to simply read an Xbox/360 DVD in
an ordinary computer's DVD-ROM drive. The optical drives in Microsoft 
consoles have special firmware which allows them to access areas of the 
disc that are effectively invisible to most DVD-ROM drives. In order to 
mount a filesystem, generally, you will have to rip the proper 
sector image from the disc using special hardware and tools, or contact 
another source who has already done so.

Note also that there are likely to be bugs and perhaps even security 
problems. xbfuse is currently meant as primarily an experimental 
research tool for studying Microsoft Xbox/360 discs.


Requirements:
```
	- Linux 2.4.x or 2.6.x (as of 2.6.14 FUSE is part of the
	  kernel, but you still need user libraries)
	- FUSE (http://fuse.sourceforge.net) 2.5.x or higher
```

Build:
```
	./configure && make
```

Install:
```
	make install
```

Usage:
```
	xbfuse <image_file> <mount_point>

	To unmount previously mounted file, use:
	fusermount -u <mount_point>

	To debug, or investigate how xbfuse examines the filesystem:
	xbfuse <image_file> <mount_point> -d
```
