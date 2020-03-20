## General Usage Steps

### 1. Download or build the binary
Download the `webp-server` from [release](https://github.com/n0vad3v/webp_server_go/releases) page.

Wanna build your own binary? Check out [build](#build-your-own-binaries) section

### 2. Dump config file

```
./webp-server -dump-config > config.json
```

The default `config.json` may look like this.
```json
{
	"HOST": "127.0.0.1",
	"PORT": "3333",
	"QUALITY": "80",
	"IMG_PATH": "/path/to/pics",
	"EXHAUST_PATH": "/path/to/exhaust",
	"ALLOWED_TYPES": ["jpg","png","jpeg"]
}
```

Regarding the `IMG_PATH` section in `config.json`. 
If you are serving images at `https://example.com/pics/tsuki.jpg` and your files are at `/var/www/image/pics/tsuki.jpg`, then `IMG_PATH` shall be `/var/www/image`.

`EXHAUST_PATH` is cache folder for output `webp` images, with `EXHAUST_PATH` set to `/var/cache/webp` 
in the example above, your `webp` image will be saved at `/var/cache/webp/pics/tsuki.jpg.1582558990.webp`.

### 3. Run

```
./webp-server --help
Usage of ./webp-server:
  -child
        is child process
  -config string
        /path/to/config.json. (Default: ./config.json) (default "config.json")
  -dump-config
        Print sample config.json
  -dump-systemd
        Print sample systemd service file.
  -jobs int
        Prefetch thread, default is all. (default 8)
  -prefetch
        Prefetch and convert image to webp
  -prefork
        use prefork
```
#### Prefetch
Prefetch will convert all your images to webp. Don't worry, WebP Server will start, you don't have to wait until prefetch completes.
```
./webp-server -prefetch
```
If you want to control threads to use while prefetching, add `-jobs=4`. 
By default, it will utilize all your CPU cores.
```
# use 4 cores
./webp-server -prefetch -jobs=4
```

#### dump systemd service file
The standard systemd service file will show on your screen. You may want to use `>` to redirect to a file.

```
./webp-server -dump-systemd
```

#### screen or tmux
Use `screen` or `tmux` to avoid being terminated. Let's take `screen` for example
```
screen -S webp
./webp-server --config /path/to/config.json
```
(Use Ctrl-A-D to detach the `screen` with `webp-server` running.)

#### systemd
Don't worry, we've got you covered!

Download `webp-server` to `/opt/webps/webp-server`, and create a config file to `/opt/webps/config.json`, then,

```shell script
./webp-server -dump-systemd > /lib/systemd/system/webp-server.service
systemctl daemon-reload
systemctl enable webp-server.service
systemctl start webp-server.service
```

#### docker

We've build docker images on [hub.docker.com](https://hub.docker.com/repository/docker/webpsh/webps). If you want to run webp-server insider docker container, you can run the command below,
```shell
docker run -d -p 3333:3333 -v /path/to/pics:/opt/pics --name webps webpsh/webps
```
The path `path/to/pics` is your images serving in local. The path `/opt/pics` unable modify because it define in the `config.json` when building docker image. The cache folder of `EXHAUST_PATH` default define in `/opt/exhaust` , you can also mount the local dir for the cache folder by using `-v /path/to/exhaust:/opt/exhaust` option.

### 4. Nginx proxy_pass
Let Nginx to `proxy_pass http://localhost:3333/;`, and your webp-server is on-the-fly.