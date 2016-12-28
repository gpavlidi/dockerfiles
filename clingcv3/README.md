# clingcv
[cling](https://root.cern.ch/cling) is a C++ [repl](https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop). Imagine irb but for C++ with OpenCV 2 support.

### Usage

After **docker pull gpavlidi/clingcv**, these 2 aliases in a bash_profile might come in handy:

- clingcv: C++ console with most frequent headers loaded
```
alias cling='docker run -it --rm gpavlidi/cling -Wc++11-extensions -std=c++11 -liostream -lvector -lstring -lunordered_map -lqueue -lstack -lalgorithm' 

```

- clingcvx: C++ console same as cling but with x11 forwarding too! To get docker X11 forwarding working, check out [this](http://blog.ctaggart.com/2016/03/gnu-octave-via-docker-x11.html?m=1)
```
alias clingx="xhost + $(dinghy ip) && ip=$(ifconfig vboxnet0 | grep inet | awk '$1=="inet" {print $2}') docker run -it --rm -e DISPLAY=${ip}:0 -v /tmp/.X11-unix:/tmp/.X11-unix gpavlidi/cling -Wc++11-extensions -std=c++11 -liostream -lvector -lstring -lunordered_map -lqueue -lstack -lalgorithm"

```
