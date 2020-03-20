# Prefetch

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
