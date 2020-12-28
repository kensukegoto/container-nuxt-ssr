# node上でNuxtを動かす

## 参考

- [nuxt.jsのDocker開発環境](https://odaryo.hatenablog.com/entry/2019/12/05/104305)
- [nuxtのSSRをdockerに乗せてデプロイする方法](https://forum.vuejs.org/t/nuxt-ssr-docker/34279/2)


## ポイント

### nuxt.config.jsに"host"の設定をする

#### 参考

https://ja.nuxtjs.org/faq/host-port/<br>
<br>
package.jsonで設定する事も出来そう。

#### サンプル

デフォルトではlocalhostとなり、ホストマシン内からのみアクセス可能。コンテナの外に向けるには、0.0.0.0を設定する。

```
  server: {
    port: 3000,
    host: '0.0.0.0',  // <- これ!
  },
```

### .dockerignoreでビルドに不要なファイルを除外

node_modulesと.nuxtをCOPYに含めたく無い。.dockerignoreに記載すると除外してくれる。

## 基本コマンド

```
# ビルド

docker build -t nuxt-container:1.0 .

# コンテナ起動

docker run -d -p 3000:3000 --name nuxt-app --rm nuxt-container:1.0

# コンテナに入りたい

docker ps # コンテナIDを調べる
docker exec -it コンテナID /bin/bash

```