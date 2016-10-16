# clingcv
[cling](https://root.cern.ch/cling) is a C++ [repl](https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop). Imagine irb but for C++ with OpenCV 2 support.

### Usage

After **docker pull gpavlidi/clingcv**, these 2 aliases in a bash_profile might come in handy:

- clingcv: C++ console with most frequent headers loaded
```
alias clingcv='docker run -it --rm gpavlidi/clingcv -Wc++11-extensions -std=c++11 -liostream -lvector -lstring -lunordered_map -lqueue -lstack -lalgorithm -lopencv2/opencv.hpp -lopencv_calib3d -lopencv_contrib -lopencv_core -lopencv_features2d -lopencv_flann -lopencv_gpu -lopencv_highgui -lopencv_imgproc -lopencv_legacy -lopencv_ml -lopencv_objdetect -lopencv_ocl -lopencv_photo -lopencv_stitching -lopencv_superres -lopencv_ts -lopencv_video -lopencv_videostab -L/usr/lib/x86_64-linux-gnu/'

```

- clingcvx: C++ console same as cling but with x11 forwarding too! To get docker X11 forwarding working, check out [this](http://blog.ctaggart.com/2016/03/gnu-octave-via-docker-x11.html?m=1)
```
alias clingcvx="xhost + $(dinghy ip) && ip=$(ifconfig vboxnet0 | grep inet | awk '$1=="inet" {print $2}') docker run -it --rm -e DISPLAY=${ip}:0 -v /tmp/.X11-unix:/tmp/.X11-unix gpavlidi/clingcv -Wc++11-extensions -std=c++11 -liostream -lvector -lstring -lunordered_map -lqueue -lstack -lalgorithm -lopencv2/opencv.hpp -lopencv_calib3d -lopencv_contrib -lopencv_core -lopencv_features2d -lopencv_flann -lopencv_gpu -lopencv_highgui -lopencv_imgproc -lopencv_legacy -lopencv_ml -lopencv_objdetect -lopencv_ocl -lopencv_photo -lopencv_stitching -lopencv_superres -lopencv_ts -lopencv_video -lopencv_videostab -L/usr/lib/x86_64-linux-gnu/"

```
