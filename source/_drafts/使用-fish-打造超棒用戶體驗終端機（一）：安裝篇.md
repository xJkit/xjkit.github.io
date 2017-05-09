---
title: 使用 fish 打造超棒用戶體驗終端機（一）：安裝篇
tags:
---

![使用 fish shell 打造超棒用戶體驗終端機](banner-fish.svg)

~~好的終端機帶你上天堂~~，為了加速你的工作效率，你一定要試試 [fish](https://fishshell.com/) shell。全名為 **F**riendly **I**nteractive **Sh**ell，跟當紅的 **bash** 與 **zsh** 相比算是小眾，但由於它一裝完「原廠」即有超優使用者體驗，造福那些不需要高度訂製 .bashrc 或 .zshrc 設定檔的懶人來說非常方便，因為無需設定就非常好用，你一定會愛死它。

<!-- more -->

![fish shell 超方便自動補齊](fish-autocomplete-demo.gif)

fish 擁有超強自動補齊的功能，透過歷史紀錄來瞭解你的語法，在重複敲進相同指令時會提出建議，建議的字體以灰色顯示。不僅如此，在使用指令時會變色，預知你指令是否正確。說了這麼多，先來搞安裝，不會太久。

# 安裝 fish shell

我個人使用 Mac OS 蘋果作業系統，而且 fish 在 Mac 上面運作的非常好，再次以此平台展示安裝，其他平台可參見 [fish 官方網站](https://fishshell.com/)。Mac 上直接使用 [Homebrew](https://brew.sh/) 安裝整個快到不行：

```sh
brew install fish
```

安裝完畢。鍵入 `fish` 就可以看見你的 bash 變成了 fish！

由於 Mac 作業系統預設使用 bash，若每次打開新的終端機都要 key 一次 `fish` 豈不是挺累人的。如果你使用 fish 後發現體驗很棒，想要終端機預設 fish，請繼續看下去。

## 使用 fish 作為你的預設 shell

Mac 所有的 shell 都條列在 `/etc/shells` 檔裡面。你會發現裡面除了 **bash** 和 **zsh** 之外，另有 ksh, csh, tcsh 等。以上都不是重點，你只要把你剛剛透過 **brew** 安裝的 fish 路徑放在最後一行：

```sh
/bin/bash
/bin/csh
/bin/ksh
/bin/sh
/bin/tcsh
/bin/zsh
/usr/local/bin/fish # 新增你的 fish 在這裡
```

接著，使用 `chsh` 改變你的預設 shell:

```sh
chsh -s /usr/local/bin/fish
```

設定完畢。打開一個新的終端機，你會第一眼看見 fish。

## 定製你的 fish shell

fish 預設的設定檔案位於 `~/.config/fish/config.fish`，在 fish 啟動時都會讀取一遍。你可以在上面自定歡迎畫面，例如：

```sh
  echo "Welcome to j fish"
```

這段話就會在沒當你開啟 fish 時自動顯示。另外，你也可以自己定義 function ，每當開啟 fish 就可以使用。

嫌設定檔麻煩嗎？ fish 提供了一個網頁版 UI 頁面讓你開心做設定，只要在 fish shell 下輸入：

```sh
$ fish_config

Web config started at 'file:///Users/JoeyChung/.cache/fish/web_config-8TAAZN.html'. Hit enter to stop.
```


你會發現瀏覽器自動開啟 `http://localhost:8000`，便可進入到網頁版 fish 設定頁面，非常方便。

## 安裝 fish 套件管理系統：[oh-my-fish](https://github.com/oh-my-fish/oh-my-fish)

[oh-my-fish](https://github.com/oh-my-fish/oh-my-fish) 或 **omf** 是為了進一步強化 fish shell 功能的套件管理器，就像使用 **zsh** 會安裝 [oh-my-fish](https://github.com/robbyrussell/oh-my-zsh)。讓你覺得還不滿足現在好用的 fish。

