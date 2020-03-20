# WebP Server Go

<p align="center">
	<img src="./pics/webp_server.png"/>
</p>
<img src="https://api.travis-ci.org/webp-sh/webp_server_go.svg?branch=master"/>

This is a Server based on Golang, which allows you to serve WebP images on the fly. 
It will convert `jpg,jpeg,png` files by default, this can be customized by editing the `config.json`.. 
* currently supported  image format: JPEG, PNG, BMP, GIF(static image for now)


> e.g When you visit `https://a.com/1.jpg`，it will serve as `image/webp` without changing the URL.
>
> For Safari and Opera users, the original image will be used.