# Basic Usage

## Download or build the binary
Download the `webp-server-go` from [release](https://github.com/webp-sh/webp_server_go/releases) page.

## Dump config file

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

## Run

```
./webp-server --config=/path/to/config.json
```