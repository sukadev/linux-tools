
myphoto
=======

    Move JPEG files to a directory tree based on the date the pictures
    were taken. For a picture taken on on March 1, 2020, with a camera
    nickname (see below) "My-Canon-T3", the destination path name of
    the JPEG will be:

        ${Topdir}/2020/2020-0301-My-Canon-T3/IMG_1234.JPG

    where "Topdir" could be, "/home/user1/Photos/"

    In addition to the JPEG file (or a directory of JPEG files) a few
    simple inputs are needed which must be specified via environment
    variables which are described below.

    If the destination file already exists, the tool will report whether
    its a duplicate or a collision (a different file with same basename)
    and will not perform the move. The detection is based on md5sum.

    .. code::

        myphoto [operation] <argument>

            Perform the operation on the specified argument. If operation
            is not specified, show-dest is assumed. argument should be a
            single JPEG file or the root a directory tree containing the
            JPEG files to be processed. Valid operations are shown below.

        myphoto show-dest IMG_1234.JPG

            Show destination that JPEG would be moved to. Do not perform
            move.

        myphoto check-dest IMG_1234.JPG

            Report if JPEG file can be moved to its destination. Do not
            perform the move. If reporting UNKNOWN-CAMERA, report [make,
            model, serial] of the camera used to create the JPEG file.

            DUPLICATE       Destination exists and is identical (md5sum)
            COLLISION       Destination exists and is different (md5sum)
            UNKNOWN-CAMERA  No nick name for camera.
            SUCCESS         Can be safely moved

        myphoto.py move-jpeg IMG_1234.JPG

            Move JPEG the file - assuming no errors like the ones reported
            by check-dest

        myphoto.py help

            Print some help about the tool (TODO)


Environment variables
---------------------

    `export MYPHOTO_TOP_DIR`

        Set to the root of the destination directory tree where the JPEG files
        should be moved to. Eg: "/home/user1/myphotos/Photos/"

    `export MYPHOTO_LOG_DIR`

        Set to the directory where log file should be saved. The log file
        will contain at least one line per file processed and maybe useful
        to save for later use. Eg: "/home/user1/myphotos/logs/"

    `export MYPHOTO_CAMERA_LIST`

        Path name of the camera list (see Camera List)
        Eg: "/home/user1/myphotos/camera-list"

Camera List
-----------
   To avoid collision between pictures taken by different cameras, the path
   name of the destination includes a nick name of the camera. The nick names
   should be specified in a simple file like:

   .. code::

        $ cat /home/user1/myphotos/camera-list

        123456789012 : User1-Canon-T3
        987656789012 : User2-Canon-T3
        # A cell phone
        764533289012 : User2-Samsung-S3

   Format is one line per camera, with camera serial number, followed by
   a single colon followed by a nick name. No spaces in serial number or
   nick name. Blank lines and lines with # in first column are ignored.

   You can find the camera details (Make, Model, Serial) of a JPEG file by
   running:

   .. code::

        $ myphoto check-dest IMG_1234.JPG
        IMG_1234.JPG: [UNKNOWN-CAMERA (Canon, Canon-EOS-REBEL-T3, 123456789012]

TODO
----

    - Allow multiple arguments per invocation - we only allow one JPEG file or
      one directory at present.
    - Implement `myphoto help`
