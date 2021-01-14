Good day

I created this mini project as I wanted to help a family member to convert images to svg. 


TLDR: We want to convert an image (likely to be JPG / PNG) to a SVG file whilst not exceeding the maximum file size limit of most websites. 

Note to self, there are 3 steps to this process: 
1) Convert the JPG / PNG file to a SVG file
2) Optimize the SVG file
3) Zip the SVG file -> SVGZ 

#1: CONVERT THE IMG FILE TO SVG: 

Checklist: 
[X] Works with JPEG 
[x] works with PNG (+= 24bits)

To solve this, I looked to the internet. No point re-inventing the wheel right? 

Check the file 
    convert_image_to_vector.py 
to see the code I found online to solve this problem. 

Src: https://programmersought.com/article/82275414845/

As per the website, please take note of this: 

"When performing pixel vector conversion, the picture mode only supports RGB three-color mode. Take png as an example. If it is a full-color 24-bit image, it is supported, but an 8-bit png image Obviously it cannot be converted because its picture mode is P mode. In this case, before using python script to convert the picture, it is recommended to use photoshop to perform a simple mode conversion on the picture."

So please take a look at their website if you need more assistance with this. 

#2: OPTIMIZE THE SVG FILE:

Our SVG file will be huge -> downside of SVG files in general. We can, however, remove some unnecessary metadata and formatting. 
One way to do this, is to use: 

Scour 
    - "Scour is an SVG optimizer/cleaner that reduces the size of scalable vector graphics by optimizing structure and removing unnecessary data written in Python." 
    (src="https://github.com/scour-project/scour")

    -   Code run in Commandline: 
    scour -i butterfly.svg -o test_vector.svg --enable-viewboxing --enable-id-stripping --enable-comment-stripping --shorten-ids --indent=none

-   a 32M svg file became 25M. 

#3: ZIP THE SVG FILE

## Using Mac OS X AND in Unix-Linux:
-   tar czf archive_folder_name.tar.gz folder_to_copy
Replace archive_folder_name.tar.gz with whatever you want to call the newly created archive, and folder_to_copy with whatever is the name of the folder you want to archive.

src="https://superuser.com/questions/46512/create-a-tar-file-for-compressing-files-and-directories-on-mac-os-x"

Src="https://mkyong.com/linux/how-to-zip-unzip-tar-in-unix-linux/"

EG: tar czf compressed_butterfly.tar.gz butterfly.svg

IF you want to compress even further, there is another option: bzip2

bzip2:
    src="https://www.howtogeek.com/248780/how-to-compress-and-extract-files-using-the-tar-command-on-linux/"

Warning: 
-   It's a lot slower
-   It's not always supported, depending on version of operating system

Advantage: 
-   it compresses a bit more, giving you a smaller file

To do so, just replace the -z for gzip in the commands here with a -j for bzip2.

EG: 
    tar -cjvf butterfly2.tar.bz2 butterfly.svg

*** Note: This compressed a 32M svg file down to 1.4M!!! 

time stats:
    6.76s user 0.07s system 96% cpu 7.069 total



