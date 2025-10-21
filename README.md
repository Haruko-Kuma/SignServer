# Linux QQ SignServer

This project can only be used on Linux.

## How to use?

First, go to the official website to download deb file of the QQ, and rename it to `linuxqq.deb`.

I recommend downloading the Linux x64 3.2.19-39038 version. If you want use another version, go to visit [Config section](#config).

And then:

```sh
ar -p linuxqq.deb data.tar.xz | tar -xJ ./opt/QQ/resources/app/wrapper.node -O > wrapper.node && rm linuxqq.deb

patchelf \
--remove-needed libbugly.so \
--remove-needed libX11.so.6 \
--remove-needed libX11-xcb.so.1 \
--remove-needed libXext.so.6 \
--remove-needed libvips-cpp.so.42 \
--add-needed libstdc++.so.6 \
--add-needed libsymbols.so \
wrapper.node
```

If you have Docker, you may refer to the [Docker section](#docker) for further information.

```sh
gcc -std=c99 -shared -fPIC -o libsymbols.so symbols.c

cargo run --release
```

The server will listen on `127.0.0.1:8080`. If you want to listen on other endpoints, go to modify the `sign.config.toml` file.

Enjoy!

## Docker

```sh
docker build -t sign-server:1.2.0 .

export HOSTDIR=/data/app # Or any path that you prefer

mkdir $HOSTDIR

cp wrapper.node sign.config.toml $HOSTDIR

sed -i 's/127.0.0.1/0.0.0.0/g' $HOSTDIR/sign.config.toml

docker run -d --name my-sign-server -v $HOSTDIR:/app -p 127.0.0.1:8080:8080 sign-server:1.2.0
```

## Config

Modify the `sign.config.toml` file according to your needs.

If you use other versions of QQ, put `{version}.json` in the same directory. For specific content, refer to `src/appinfo/3.2.19-39038.json`.


## Praise the spirit of open source

Praise the open-source spirit of our great master 祈洱

Here is the QQ contact information of the expert: 2956419803

<img width="477" height="509" alt="QQ_1760946991307" src="https://github.com/user-attachments/assets/1f41cc81-0750-4c30-8fbd-2435d55109c7" />

Github: [AkariYau](https://github.com/AkariYau)

frame-up scene：
<img width="2080" height="952" alt="image" src="https://github.com/user-attachments/assets/d380475b-e1a2-496d-bace-7ccd83915349" />

