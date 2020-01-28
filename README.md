# JupiterFund workspace template

[![Docker Pulls](https://img.shields.io/docker/pulls/kevinprotoss/jupiter-workspace-template.svg)](https://hub.docker.com/r/kevinprotoss/jupiter-workspace-template/)
[![Build Status](https://travis-ci.com/kevinprotoss/jupiter-workspace-template.svg?branch=master)](https://travis-ci.com/kevinprotoss/jupiter-workspace-template)

### How to use

Use docker image

```
docker run -d -p 8888:8888 kevinprotoss/jupiter-workspace-template jupyter notebook --ip 0.0.0.0 --port 8888
```

Build local and start user session

```
# Use existing user id and user name on the host
docker run --rm -d -v /var/run/docker.sock:/var/run/docker.sock jupyter/repo2docker:0.10.0-127.gd9335cf jupyter-repo2docker --user-id 1000 --user-name junxiang --image-name kevinprotoss/jupiter-workspace-template --publish 8888 https://github.com/kevinprotoss/jupiter-workspace-template
```

### More configurations

The jupyter notebook workspace needs sometimes more dependencies, such as jupiterapis. These dependencies are built and updated automatically on the jupiter server and mounted then into the persisted docker volume `share-lib`.

```
# Use existing `share-lib` volume already on the host
-v share-lib:/share-lib
```

So as to import the python packages into the workspace immediately after user session starts, additional path must be appended into `PYTHONPATH` by means of:
   
* Run command
  ```
  docker run -d -p 8888:8888 -v share-lib:/share-lib kevinprotoss/jupiter-workspace-template bash -c "exec env PYTHONPATH=${PYTHONPATH}:/share-lib jupyter notebook --ip 0.0.0.0 --port 8888"
  ```

* `postBuild` script
  ```
  export PYTHONPATH="/share-lib:$PYTHONPATH"
  ```

