# JupiterFund workspace template

### How to use

```
docker run -d -v /var/run/docker.sock:/var/run/docker.sock jupyter/repo2docker:0.10.0-127.gd9335cf jupyter-repo2docker --user-id 1000 --user-name junxiang --image-name kevinprotoss/jupiter-workspace-template --publish 8888 https://github.com/kevinprotoss/jupiter-workspace-template
```