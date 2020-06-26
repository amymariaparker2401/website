# 🔥 Hot Module Replacement

Hot Module Replacement（HMR）は、ページ全体を更新しなくても、実行時にブラウザ内のモジュールを自動的に更新することで開発者体験を向上させる仕組みです。これは、変更を行ってもアプリケーション内の状態（ステート）は保持されることを意味します。Parcel の HMR 実装は、そのままで JavaScript と CSS の両方をサポートします。プロダクションモードでバンドルすると、HMR は自動的に無効になります。

ファイルを保存すると、Parcel は差分をリビルドし、新しいコードを含んでいる実行中のクライアントに更新を知らせます。その後、新しいコードは古いバージョンを置き換え、すべての親要素と共に再評価されます。モジュールが破棄されようとしているとき、または新しいバージョンに更新されるとき、コードに通知することが出来る `module.hot` API を使用することで、このプロセスにフックすることができます。[react-hot-loader](https://github.com/gaearon/react-hot-loader) のようなプロジェクトはこのプロセスを手助けすることができ、Parcel なら設定不要で使用できます。

知っておくと良い方法が 2 つあります： `module.hot.accept` と `module.hot.dispose` です。`module.hot.accept` は、あるモジュールまたはその依存関係のいずれかが更新されたときにコールバック関数が実行されます。`module.hot.dispose` は、あるモジュールが置き換えられようとしているときにコールバック関数が実行されます。

```javascript
if (module.hot) {
  module.hot.dispose(function() {
    // module is about to be replaced
  })

  module.hot.accept(function() {
    // module or one of its dependencies was just updated
  })
}
```

## 依存関係の自動インストール

Parcel は必要なモジュールが `node_module` フォルダーに存在しない状況に出くわした場合はいつでも、それらを自動でインストールしようとする仕組みがあります。これは、yarn.lock ファイルが見つかるかどうかによって、`yarn` か `npm` を用いて行います。これによって、開発者は一度ターミナル上で Parcel から exit したり、複数のターミナルを立ち上げる必要がなくなります。

これらは 開発環境 \([`serve`](cli.md#serve) もしくは [`watch`](cli.md#watch) コマンド\) 時に適用されます。しかしながら、プロダクション環境（[`build`](cli.md#build) コマンド）時には、デプロイ時の予期しない副作用を回避するために無効化されています。

あなたは [`--no-autoinstall`](cli.md#disable-autoinstall) オプションを使うことでこの機能を無効化することができます。

## セーフライト

IDE やテキストエディタの中には、`セーフライト（safe write）`と呼ばれる、データの損失を防ぐためにコピーを取り保存時に名前を変更するという機能があります。

ホットモジュールリプレイスメント（HMR）を使用している場合、この機能はファイル更新の自動検出をブロックしてしまうので セーフライトを無効にするためには、下記のオプションを使用します。

* `Sublime Text 3` `atomic_save: "false"` を preferences に追加する。
* `IntelliJ` preferences 内で "safe write" を検索し、無効化する。
* `Vim` `:set backupcopy=yes` を設定に追加する。
* `WebStorm` Preferences &gt; Appearance & Behavior &gt; System Settings 内の `Use "safe write"` のチェックを外す。

