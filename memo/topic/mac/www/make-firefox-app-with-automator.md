<!-- -*- coding: utf-8 -*- -->

# Mac で Automator を使って Firefox を複数プロファイル起動

アイコンの変更方法は忘れた. 後で書くかも.

#### 1.
```shell-script
$ /Applications/Firefox.app/Contents/MacOS/firefox -ProfileManager
```
などとして `~/Library/Application\ Support/Firefox/Profiles/` に `mail`, `prog`, `tmp`
というプロファイルを作ったとする.

#### 2.
以下の様な `~/bin.darwin/firefox-trampoline` を用意しておく.

```shell-script
#! /usr/bin/env bash

FIREFOX="/Applications/Firefox.app/Contents/MacOS/firefox"
PROFILEDIR="$HOME/Library/Application Support/Firefox/Profiles"

$FIREFOX --no-remote --profile "$PROFILEDIR/$1" &> /dev/null &
```

#### 3.
Automator を開く.

#### 4.

"アクション" > "シェルスクリプトを実行"

#### 5.

```shell-script
~/bin.darwin/firefox-trampoline mail
```

などと書く. shell は `/bin/bash` でよい.

#### 6.

Command-S で保存.

`~/bin.local/automator/` 以下に `firefox-mail.app` などで保存しておいて,

```shell-script
$ (cd /Applications ;  ln -s ~/bin.local/automator/firefox-mail.app )
```

とかしておくと Launchpad が launcher になってべんり.
