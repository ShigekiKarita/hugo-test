---
title: "My First Post"
date: 2019-04-29T12:56:42+09:00
draft: false
---

Hugo使ってみたかったが、D言語のシンタックスハイライトがなかったのでPRおくってみた

https://github.com/alecthomas/chroma/pull/249

マージされたので、そのうち新バージョンがリリースされて Hugo 本家にもアップデートされると思うが、とりあえず fork してアップデートしてみた。

```d
import std.stdio;
void main() {
    writeln("Hello");
}
```

ちゃんとハイライトされていると思う。

```yaml
sudo: false
language: go
script:
  # install hugo
  - INIT_DIR=$(pwd)
  - mkdir $HOME/src
  - cd $HOME/src
  - git clone https://github.com/ShigekiKarita/hugo --depth 1 -b dlang
  - cd hugo
  - go install
  - cd $INIT_DIR
  # build page
  - $GOPATH/bin/hugo
  - touch public/.nojekyll

deploy:
  provider: pages
  skip_cleanup: true
  github_token: $GITHUB_TOKEN # Set in travis-ci.org dashboard
  local_dir: public
  on:
    branch: master
```

こんな風にTravisを設定してgh-pages上にデプロイしたのがこのページである。

- https://docs.travis-ci.com/user/deployment/pages/
- https://github.com/ShigekiKarita/hugo-test/blob/master/.travis.yml

それか、私の作ったバイナリを信用するならもっと楽である。

```yaml
sudo: false
language: bash
script:
  - wget https://github.com/ShigekiKarita/hugo/releases/download/dlang-v1/hugo.tar.xz
  - tar -xvf hugo.tar.xz
  - ./hugo
  - touch public/.nojekyll

deploy:
  provider: pages
  skip_cleanup: true
  github_token: $GITHUB_TOKEN # Set in travis-ci.org dashboard
  local_dir: public
  on:
    branch: master
```
