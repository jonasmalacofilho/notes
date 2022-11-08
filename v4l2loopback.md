# V4l2loopback webcam

## Connect to phone

```
$ adb start-server
$ adb forward tcp:9009 tcp:9009
```

## Set up v4l2loopback

```
# modprobe v4l2loopback exclusive_caps=1
$ ffmpeg -i http://localhost:9009/video -vf format=yuv420p -f v4l2 /dev/video0
```

## Cleanup

```
$ adb forward --remove tcp:9009
# modprobe -r v4l2loopback
```

## References

- [ipwebcam-gst](https://github.com/agarciadom/ipwebcam-gst)
- [ArchWiki: Webcam setup](https://wiki.archlinux.org/title/Webcam_setup)
