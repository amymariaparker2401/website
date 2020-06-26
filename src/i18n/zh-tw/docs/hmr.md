# 🔥 模組熱替換

模組熱替換 \(HMR, Hot Module Replacement\) 可提升你的開發效率，模組熱替換並不會重整頁面，而是即時地更新瀏覽器中的模組，讓你得以在更動某些小地方時仍可保留原本的狀態。

Parcel 內建支援 JavaScript 及 CSS 的模組熱替換，在 production 模式中將會自動停用此功能。

Parcel 會在你更動檔案時重新編譯更動的部分，並將更新發送至所有正在執行的用戶端，使用新的程式碼來替換舊版本，同時也將重新評估所有父元件是否需要更新。你可以使用 `module.hot` API 來涉入這個過程，它可以在模組即將被處理或有新版本傳入時通知你的程式。Parcel 支援了 [react-hot-loader](https://github.com/gaearon/react-hot-loader) 等專案以協助達成這個過程。

Parcel 提供了兩個方法：`module.hot.accept` 及 `module.hot.dispose`，前者能在模組或其相依套件更新時執行回呼函式，後者則在模組即將被替換時執行回呼函式。

```javascript
if (module.hot) {
  module.hot.dispose(function() {
    // 模組即將被替換
  })

  module.hot.accept(function() {
    // 模組或其相依套件剛剛更新
  })
}
```

## 自動安裝相依套件

為了讓開發者可以不用離開 Parcel 或開啟多個終端機視窗， Parcel 在 `node_modules` 中找不到相依套件時，會自動嘗試使用 `yarn` 或 `npm` 來安裝（取決於是否有 `yarn.lock` 這個檔案）。

此功能只會在 _development_ （使用 [`serve`](cli.md#serve) 或 [`watch`](cli.md#watch) 時）環境中啟用，在 _production_ （使用 [`build`](cli.md#build) 時）環境時則會自動停用此功能以避免不必要的副作用。

你可以透過 [`--no-autoinstall`](cli.md#disable-autoinstall) 選項停用此功能。

## 安全寫入

有些文字編輯器和 IDE 提供 `安全寫入` 功能，此功能基本上是在存檔時另外複製一份檔案並重新命名，以此避免資料的遺失。但使用`安全寫入`時， 模組熱替換的檔案更新偵測會被此功能阻礙，若要停用`安全寫入`可透過下列的設定方法：

* `Sublime Text 3`：在設定中增加 `atomic_save: "false"`。
* `IntelliJ`：在設定中搜尋 "safe write" 並停用。
* `Vim`： 在設定中新增 `:set backupcopy=yes`。
* `WebStorm`：在 Preferences &gt; Appearance & Behavior &gt; System Settings 中取消勾選 `Use "safe write"`。

