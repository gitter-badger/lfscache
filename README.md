# lfs-cache

[![Join the chat at https://gitter.im/lfscache/community](https://badges.gitter.im/lfscache/community.svg)](https://gitter.im/lfscache/community?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

lfs-cache is a caching proxy for [Git LFS](https://git-lfs.github.com/) servers.

## Usage

#### Docker

```
$ docker run --name lfscache --rm -d -v /my/cache/dir/lfs:/lfs saracen/lfscache:latest --url github.com/org/repo.git/info/lfs --http-addr :80  --directory /lfs
```

#### Binary

Download the correct [binary](https://github.com/saracen/lfscache/releases) for your system.

```
$ ./lfscache --url github.com/org/repo.git/info/lfs --directory /my/cache/dir/lfs --http-addr=:9876
```

`--directory` specifies the cache directory. The layout is the same used by the
Git LFS client, so it might be a good idea to copy over your `.git/lfs/objects`
directory to preload the cache (`cp -r .git/lfs/objects /my/cache/dir/lfs`).
The `tmp` and `incomplete` directories do not need to be copied over.

Now you need to have your Git LFS client point to the proxy. One method of
doing this is to replace the URL at a global level, so that it works whenever
a repository references your target LFS server.

```
git config --global url.http://my-cache-proxy:9876/.insteadOf https://github.com/org/repo.git/info/lfs
```
