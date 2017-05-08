---
title: 使用 fish shell 打造超棒使用者體驗的終端機
tags:
- shell
- git
---

# fish 在 Mac OS 下的安裝

# 使用 fish 指令範例：快速刪除多個 git branch

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