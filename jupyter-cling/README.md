# jupyter-cling

A jupyter notebook with C++ support. Great way to brush up on C++ coding/algo puzzles.
Forked from [DannyHavenith/jupinger](https://github.com/DannyHavenith/jupinger) with minor changes to support jupyter lab instead of notebook.

### Use

```
# build image
docker build --force-rm -t gpavlidi/jupyter-cling .

# default settings
docker run -it --rm -p 8888:8888 -v ~/Code/Notebooks:/usr/src/notebooks gpavlidi/jupyter-cling

```
