---
title: "My First Post"
date: 2019-04-29T12:56:42+09:00
draft: false
---

Hugo使ってみたかったが、D言語のシンタックスハイライトがなかったのでPRおくってみた

https://github.com/alecthomas/chroma/pull/249

マージされたので、そのうち新バージョンがリリースされて Hugo 本家にもアップデートされると思うが、とりあえず fork してアップデートしてみた。

```yaml
sudo: false
language: go
script:
  - unset $GOPATH
  - go get 
  - git clone https://github.com/ShigekiKarita/hugo -b dlang --depth 1
  - cd hugo && go install && cd -
  - ~/go/bin/hugo
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

ちゃんとハイライトされていると思う。

```d
import std.stdio;
void main() {
    writeln("Hello");
}
```
