### example

```
$ docker run \
  -v $HOME/go:/go \
  -v $HOME/.ssh:/root/.ssh \
  -v $HOME/.gitconfig:/root/.gitconfig \
  -p 8080:8080 \
  -e USERNAME=myusername \
  -e PASSWORD=mypassword \
  koid/cloud9-golang
```
