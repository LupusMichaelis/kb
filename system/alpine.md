# Alpine

## Package management

```sh
apk search $pkgname
apk add $pkgname
```

## Configuration and stuff

Configuration tools are in a package that is not installed by default.

```sh
apk add alpine-conf
setup-timezone -z Europe/Paris
```

## App host

```sh
apk add apache2-php5
apk add php5-mysqli
```

## DB host

```sh
apk add mariadb mariadb-server-utils
```

## Symphony host

```sh
apk add php5 # For CLI composer tools
```

## Native dev machine

```sh
apk add clang alpine-sdk build-base git vim
```
