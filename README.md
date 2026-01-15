# mozc-modeless.el

Emacs用のモードレス日本語入力インターフェースです。
通常は英数入力で、`C-j` を押したときだけカーソルの直前のローマ字文字列をMozcに渡してMozcの変換モードに入ります。

> **より賢いモードレス日本語入力をお探しの方へ:**
> LLMを使った高度な日本語入力を体験したい場合は、[Sumibi](https://github.com/kiyoka/Sumibi)をご検討ください。AIによる文脈を考慮した変換候補の提供など、より洗練された入力体験を実現しています。

## 特徴

- **モードレス入力**: IMEのON/OFF切り替え不要
- **自動復帰**: 変換確定後、自動的に英数モードに戻る
- **キャンセル対応**: `C-g`で元のローマ字を復元

## 必要環境

- Emacs 29.0以上
- mozc.el
- markdown-modeのインストール

## インストール

**注意**: Emacs 29.0以上が必要です。

### 方法1: package-vc-install を使う（推奨）

Emacs 29以降では、`package-vc-install`でGitHubから直接インストールできます。

- 事前に以下を`*scratch*`バッファで実行してinstallしてください

```elisp
(package-vc-install
  '(mozc-modeless . (:url "https://github.com/kiyoka/mozc-modeless-emacs.git")))
```

- init.elに追記してください

```elisp
(use-package mozc-modeless
  :config
  (global-mozc-modeless-mode 1))
```

### 方法2: 手動でインストール

- 事前準備

```bash
mkdir -p ~/.emacs.d/site-lisp/
cd ~/.emacs.d/site-lisp/
git clone https://github.com/kiyoka/mozc-modeless-emacs.git
```

- init.elに追記してください

```elisp
(add-to-list 'load-path "~/.emacs.d/site-lisp/mozc-modeless-emacs")
(require 'mozc-modeless)
(global-mozc-modeless-mode 1)
```

## 使い方

1. ローマ字を入力: `nihongo`
2. `C-j` を押す → 変換候補表示
3. `C-j` または `SPC` で候補選択、`RET` で確定
4. 自動的に英数モードに戻る

キャンセルは `C-g`（元のローマ字を復元）

### スラッシュ区切り

`/` を使うと、その後ろの部分だけを変換できます。

```
入力: "日本語/ga" + C-j → "日本語が"
入力: "hello/world/nihongo" + C-j → "hello/world日本語"
```

`/` は変換時に自動削除されます。
