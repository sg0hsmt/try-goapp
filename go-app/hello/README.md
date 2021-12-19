# go-app Hello

[go-app](https://github.com/maxence-charriere/go-app) は Go (WebAssembly)で [PWA](https://developers.google.com/web/progressive-web-apps/) を実装するためのパッケージで、
[ドキュメントサイト](https://go-app.dev/) 自体も go-app で構築されている。

https://github.com/maxence-charriere/go-app

ブラウザ側で動く app.wasm (ファイル名固定) とそれをサーブする app.Handler() の組み合わせで動く

## Build wasm and server

ビルドには Go 1.17 以上が必要

```console
GOARCH=wasm GOOS=js go build -o ./web/app.wasm
```

```console
go build
```

## Run Server

```console
./hello
```

or

```console
go run hello.go
```

ブラウザで http://localhost:8000/ を開くと Hello Demo が動く

## Notes

wasm の実行に必要な JavaScript コードなどは go-app の app.Handler が提供している。

wasm は Service Worker がローカルストレージにキャッシュしている。
コードを変更してもキャッシュが残っていることが多いので注意が必要

app.wasm のサイズは 12908865 byte (約 12.3 MB) でかなり大きい。
wasm サイズについては Issue も立っているがすぐに改善する見込みは薄い。

https://github.com/maxence-charriere/go-app/issues/534

app.Handler.Icon.Default を設定していない場合、次の画像ファイルが使用される。

- https://storage.googleapis.com/murlok-github/icon-192.png
- https://storage.googleapis.com/murlok-github/icon-512.png

https://github.com/maxence-charriere/go-app/blob/v9.2.1/pkg/app/http.go#L206-L209

app.Handler は静的ファイルの配信をサポートしているが、ディレクトリのプレフィックスは web 固定になっている。

https://go-app.dev/architecture#static-resources
