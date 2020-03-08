# go-app Hello

[go-app](https://github.com/maxence-charriere/go-app) は Go (WebAssembly)で [PWA](https://developers.google.com/web/progressive-web-apps/) を実装するためのパッケージ

https://github.com/maxence-charriere/go-app

ブラウザ側で動く app.wasm (ファイル名固定) とそれをサーブする app.Handler() の組み合わせで動く

## Build wasm and server

ビルドには Go 1.14 以上と Go module が必要

```
$ cd app
$ GOARCH=wasm GOOS=js go build -o ../app.wasm
```

```
$ cd server
$ go build -o ../
```

## Run Server

```
$ server
```

ブラウザで http://localhost:7777/ を開くと Hello Demo が動く

## Notes

wasm の実行に必要な JavaScript コードなどは go-app の app.Handler が提供している。

app.wasm のサイズは 4344507 byte (約 4.1 MB)

wasm のビルドには Go 1.14 が必要だがサーバー側は Go 1.13 でもビルドできる。

wasm は Service Worker がローカルストレージにキャッシュしている。
コードを変更してもキャッシュが残っていることが多いので注意が必要

app.Handler.Icon.Default を設定していない場合、次の画像ファイルが使用される。

- https://storage.googleapis.com/murlok-github/icon-192.png
- https://storage.googleapis.com/murlok-github/icon-512.png

https://github.com/maxence-charriere/go-app/blob/v6.0.3/pkg/app/http.go#L135-L138

app.Handler は静的ファイルの配信をサポートしているが、ディレクトリのプレフィックスは web 固定になっている。

https://github.com/maxence-charriere/go-app/blob/v6.0.3/pkg/app/http.go#L272
