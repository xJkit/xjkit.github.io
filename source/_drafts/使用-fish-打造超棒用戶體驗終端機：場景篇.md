---
title: 使用 fish 打造超棒用戶體驗終端機：場景篇
tags:
- shell
- git
---

![使用 fish shell 打造超棒使用者體驗的終端機](fish-command.jpg)

# 在 fish 裡使用 Git

fish 的自動補齊功能是提高 shell 使用者體驗的必備良藥，想當然爾使用 **cd** 是非常的好用不在話下：

![使用 fish shell 打造超棒使用者體驗的終端機：cd](fish-cd.png)

當你鍵入 **cd** 後直接敲 **Tab** ， fish 就會直接列出當前目錄給你選。對，是給你 **選**，只要繼續 **Tab** 或是按鍵盤左右鍵都行。

想不到 fish 在 git branch 切換分支時也有同樣的效果：

![使用 fish shell 打造超棒使用者體驗的終端機：git checkout](fish-git-checkout.png)

# 使用 fish 指令：快速刪除多個 git branch

<!-- more -->

在本地端有以下 git 分支：

```sh
$ git branch

  feat/SongInfoEditModal
  feat/add-favorite
  feat/delete-multi-songs
  feat/favicon
  feat/i18n-category-pages
  feat/i18n-mgmt-modals
  feat/i18n-mgmt-search
  feat/i18n-playlist
  feat/i18n-song-table
  feat/i18n-yt-search
  feat/import-edit-on-the-fly
  feat/import-empty-job-activation
  feat/import-preview-pager
  feat/import-records
  feat/import-records-delete
  feat/import-records-detail
  feat/import-records-empty-job-activation
  feat/import-records-job-start
  feat/import-records-refresh
  feat/multi-song-meta-modal
  feat/react-intl
  feat/setting-page
  feat/singer-edit-modal
  feat/singer-id-filtering
  feat/singertype-apply
  feat/socket-preview-in-progress
  feat/song-delete
  feat/stop-preview
  feat/tutorial-link
  xJkit-feat/import-preview-pager
  * master
  refactor/header-dropdown
  update/count-api-change
  update/external-links
  update/icon-fonts-20170314
  update/readme
```

使用 `grep` 取出 `feat` 開頭分支，並使用 `-v` 選項排除 `i18n`：

```sh
$ git branch | grep 'feat' | grep -v 'i18n'

  feat/SongInfoEditModal
  feat/add-favorite
  feat/delete-multi-songs
  feat/favicon
  feat/import-edit-on-the-fly
  feat/import-empty-job-activation
  feat/import-preview-pager
  feat/import-records
  feat/import-records-delete
  feat/import-records-detail
  feat/import-records-empty-job-activation
  feat/import-records-job-start
  feat/import-records-refresh
  feat/multi-song-meta-modal
  feat/react-intl
  feat/setting-page
  feat/singer-edit-modal
  feat/singer-id-filtering
  feat/singertype-apply
  feat/socket-preview-in-progress
  feat/song-delete
  feat/stop-preview
  feat/tutorial-link
  xJkit-feat/import-preview-pager
```

設定變數，並刪除前後空白：

```sh
set x (string trim -- (git branch | grep 'feat' | grep -v 'i18n'))
```

使用 `for` 迴圈進行迭代，並刪除指定分支：

```sh
  for i in $x:
    git branch -D $i
  end
```
結果如下：

```sh
Deleted branch feat/SongInfoEditModal (was 14940a6).
Deleted branch feat/add-favorite (was f11eeef).
Deleted branch feat/delete-multi-songs (was 2b88596).
Deleted branch feat/favicon (was 111f446).
Deleted branch feat/i18n-category-pages (was 5ccbc1d).
Deleted branch feat/i18n-mgmt-modals (was abab3f5).
Deleted branch feat/i18n-mgmt-search (was 3f59b8c).
Deleted branch feat/i18n-playlist (was 0d769e9).
Deleted branch feat/i18n-song-table (was bf57943).
Deleted branch feat/i18n-yt-search (was b4a21d2).
Deleted branch feat/import-empty-job-activation (was afef531).
Deleted branch feat/import-preview-pager (was f96bcce).
Deleted branch feat/import-records (was 497f623).
Deleted branch feat/import-records-delete (was b44d557).
Deleted branch feat/import-records-detail (was 5a987c4).
Deleted branch feat/import-records-empty-job-activation (was c21e449).
Deleted branch feat/import-records-job-start (was 9521988).
Deleted branch feat/import-records-refresh (was 9f4bce7).
Deleted branch feat/multi-song-meta-modal (was 326bb87).
Deleted branch feat/react-intl (was 22fdf52).
Deleted branch feat/setting-page (was 3befda8).
Deleted branch feat/singer-edit-modal (was df4b669).
Deleted branch feat/singer-id-filtering (was b017c3a).
Deleted branch feat/singertype-apply (was e3e7267).
Deleted branch feat/socket-preview-in-progress (was c15c128).
Deleted branch feat/song-delete (was 2e288f3).
Deleted branch feat/stop-preview (was 3e821b0).
Deleted branch feat/tutorial-link (was 35893c1).
Deleted branch xJkit-feat/import-preview-pager (was d5f591b).
```

我現在本地的 git branch 乾淨多啦：

```sh
$ git branch

  feat/import-edit-on-the-fly
  fix/YouTubePlatlist-UI-fix
  fix/YoutubePlaylist-fix
* master
  refactor/header-dropdown
  update/count-api-change
  update/external-links
  update/icon-fonts-20170314
  update/readme
```

現在只要保留 `master` 與 `feat/import-edit-on-the-fly`，其他都要刪除。

使用 `grep -E` 抓取多組字串：

```sh
$ git branch | grep -E 'fix|update|refactor'

  fix/YouTubePlatlist-UI-fix
  fix/YoutubePlaylist-fix
  refactor/header-dropdown
  update/count-api-change
  update/external-links
  update/icon-fonts-20170314
  update/readme
```

一樣，先過濾前後空白，然後透過 `for` 迴圈迭代刪除這些分支：

```sh
for i in (string trim -- (git branch | grep -E 'fix|update|refactor'))
  git branch -D $i
end
```

結果如下：

```sh
Deleted branch fix/YouTubePlatlist-UI-fix (was 19fcd90).
Deleted branch fix/YoutubePlaylist-fix (was 5d695b5).
Deleted branch refactor/header-dropdown (was 173cfe9).
Deleted branch update/count-api-change (was 9d1cb2f).
Deleted branch update/external-links (was 76cf82c).
Deleted branch update/icon-fonts-20170314 (was 410a16b).
Deleted branch update/readme (was 947609e).
```

我的 git branch 已經乾淨到不行了：

```sh
$ git branch

  feat/import-edit-on-the-fly
* master
```