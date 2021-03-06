# uphold/litecoind

A litecoind docker image.

[![uphold/litecoind][docker-pulls-image]][docker-hub-url] [![uphold/litecoind][docker-stars-image]][docker-hub-url] [![uphold/litecoind][docker-size-image]][docker-hub-url] [![uphold/litecoind][docker-layers-image]][docker-hub-url]

## What is litecoind?

litecoind is a program that implements the Litecoin protocol for remote procedure call (RPC) use. For more information see _[litecoinwiki](https://litecoin.info/Litecoin)_.

## Usage

### How to use this image

This image contains the main binaries from the Litecoin Core project - `litecoind`, `litecoin-cli` and `litecoin-tx`. It behaves like a binary, so you can pass any arguments to the image and they will be forwarded to the `litecoind` binary:

```sh
$ docker run --rm -it uphold/litecoind \
  -printtoconsole \
  -regtest=1 \
  -rpcallowip=172.17.0.0/16 \
  -rpcpassword=bar \
  -rpcuser=foo
```

By default, `litecoind` will run as user `litecoin` for security reasons and with its default data dir (`~/.litecoin`). If you'd like to customize where `litecoind` stores its data, you must use the `LITECOIN_DATA` environment variable. The directory will be automatically created with the correct permissions for the `litecoin` user and `litecoind` automatically configured to use it.

```sh
$ docker run -e LITECOIN_DATA=/var/lib/litecoind --rm uphold/litecoind \
  -printtoconsole \
  -regtest=1
```

You can also mount a directory in a volume under `/home/litecoin/.litecoin` in case you want to access it on the host:

```sh
$ docker run -v ${PWD}/data:/home/litecoin/.litecoin --rm uphold/litecoind \
  -printtoconsole \
  -regtest=1
```

You can optionally create a service using `docker-compose`:

```yml
litecoind:
  image: uphold/litecoind
  command:
    -printtoconsole
    -regtest=1
```

## Supported Docker versions

This image is officially supported on Docker version 1.10, with support for older versions provided on a best-effort basis.

## License

The [uphold/docker-litecoind][docker-hub-url] docker project is under MIT license.

[docker-hub-url]: https://hub.docker.com/r/uphold/litecoind
[docker-layers-image]: https://img.shields.io/imagelayers/layers/uphold/litecoind/latest.svg?style=flat-square
[docker-pulls-image]: https://img.shields.io/docker/pulls/uphold/litecoind.svg?style=flat-square
[docker-size-image]: https://img.shields.io/imagelayers/image-size/uphold/litecoind/latest.svg?style=flat-square
[docker-stars-image]: https://img.shields.io/docker/stars/uphold/litecoind.svg?style=flat-square
