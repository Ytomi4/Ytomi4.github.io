---
title: 新しいLinuxの教科書
categories: diary
auther_staff_member: Ytomi
show_comments: true
date: 2020-09-10
---

## 三宅英明、大角祐介『新しいLinuxの教科書』(2015) 

冬草に『新しいLinuxの教科書』Kindle版が半額になっていると教えてもらい、読むことにした。

既にUbuntuはWSL上へインストールしており、Uchan C++講習会で基本的な操作は扱っていたため、復習として読んだ部分が多かったものの、体系的にまとめられた読み返せるテキストとして手元にある重要性を感じている。

lsコマンドひとつをとっても、manコマンドでマニュアルを読みながらオプションを試し、.bashrcを読みながら使用可能になっているエイリアスを確認するなど、なんとなくで使っていたコマンドを親しみをもって使えるようになった。

``` .bashrc
# some more ls aliases
alias ll='ls -alF'
alias la='ls -A'
alias l='ls-CF'
```

他にもいくつか挙げるならば、シェル変数と環境変数、標準入力と標準出力（パイプ）、プロセスとジョブの管理、パッケージとレポジトリ、などの内容が特に読みやすくまとまっていたように思う。tmuxコマンドやxargsコマンドは、知らずに過ごしていたものの、積極的に使っていこうと思ったコマンドだった。

そういえば、~/.bashrcの読み込みを確認しようと~/.profileを読んでいると、ホームディレクトリ下にユーザーが置いたbinディレクトリをPATHに追加する記述があった。

``` .profile
# set PATH so it includes user's private bin if it exists
if [ -d "$HOME/bin" ] ; then
    PATH="$HOME/bin:$PATH"
fi
```

ということで、後半の大部分を占める、シェルスクリプトの作成は本書で初めて取り組んだ内容だった。

自分自身では、ひとまず何か書いてみようと、この日記の書き出しを簡便にするため、規則に沿った.mdファイルの作成と規定の書き出しを入力したうえでvimでファイルを開くコマンドを用意した。


``` diary.sh
#!/bin/bash

directory="${HOME}/workspace/Rails/Ytomi4.github.io"
date=$(date '+%Y-%m-%d')

read -p "title: " title
read -p "categories: " category

cd "${directory}"
touch "./_posts/${date}-${title}.md"

var1=\
"---\n\
title: ${title}\n\
categories: diary\n\
auther_staff_member: Ytomi\n\
show_comments: true\n\
date: ${date}\n
---\n"

echo -e $var1 > ./_posts/${date}-${title}.md
vim ./_posts/${date}-${title}.md
```

折角なので、もう少しこまめにブログをアップしていこうと思う。
