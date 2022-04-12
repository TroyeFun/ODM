```
docker run -tid --entrypoint bash --network=host opendronemap/odm
```

In docker container
```
apt update
apt install vim
sudo vim /etc/apt/sources.list
# remove contents in the file and add tsinghua apt source (https://www.jb51.net/article/187442.htm)
apt update
apt install libgdal-dev
export https_proxy=127.0.0.1:8890  # to fanqiang
bash configure.sh install
......
```

