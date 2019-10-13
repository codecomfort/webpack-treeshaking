# 20191013

- 解説は npm だが、原則 yarn でやる

- 解説中、webpack コマンドを使っているが動作しない。
  path を通すか、npx を使ってやる。以下を参照。

  - [webpack 4 入門 - Qiita](https://qiita.com/soarflat/items/28bf799f7e0335b68186#webpack%E3%81%AE%E3%83%AD%E3%83%BC%E3%82%AB%E3%83%AB%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB)
  - [npm と webpack4 でビルド - jQuery からの次のステップ - Qiita](https://qiita.com/civic/items/82c0184bcadc50965f91)

- [GitHub - babel/babel-loader: 📦 Babel loader for webpack](https://github.com/babel/babel-loader)

- [babel-core - npm](https://www.npmjs.com/package/babel-core)  
  1 年くらい更新されていない。いまだと @babel/core か。
  とはいえ、とりあえず言うとおりにやってみる
  → @babel/core が無いというエラーが出るので、@babel を使った方がよさそう

- [babel-preset-env · Babel](https://babeljs.io/docs/en/6.26.3/babel-preset-env)  
  こちらも同様に、いまは @babel/preset-env
  また、babelrc の env という記述も、@babel/env にしないとエラーになる

## 20191013 現在、modules: false は必要なさそう

- babelrc に modules: false を記述しなくても、結果は変わらなかった
  - webpack --display-used-exports のコンソール出力、bundle.js とも変わりない(普通に tree shaking されている)

## 20191013 現在、react-bootstrap の import

- lib 以下ではなく、react-bootstrap 直下にある  
  解説の通りにやってみてもエラーになると思ったら、そもそも from 'react-bootstrap/lib/～' で import できない
- Grid は無いぽい
- そもそも default export が無くなっていて、全体インポートできない  
  → babelrc に設定を入れようが入れまいが、変化なし

## 検証結果

更新された記事はいかにも最近の記事に見えるが、実際に検証してみると記事内容が再現しないことがあり、注意が必要
ライブラリ側も随時アップデートしているため、以下の二点に気をつける

- 現時点で、普通の手順でやったら、本当に tree shaking は効いていないのか？
  - webpack やライブラリ側のアプデで、状況が変わっている可能性がある
  - 何もしないで tree shaking してくれるなら、それが一番(メンテナンスコストがなくなる)
- 手順を守っていても、変えていなくても、ライブラリ側のアプデで状況が変わっている可能性がある
  - 半年くらい経っていたらもう怪しい。一度設定したきり放置しない。
  - 定期的に、その設定(この例で言えば transform-imports まわりの設定)を有効にした場合と無効にした場合で出力サイズの比較を行い、tree shaking が効いているかどうかを確認する。また、それを自動化できればなおよし。
- その他
  - [webpack4 の Tree Shaking を基本的な import/export で試してみる - Qiita](https://qiita.com/Statham/items/22de39267c9dfca283a5)  
    この記事も興味深い。webpack4 の場合、多くのケースで tree shaking が効いてるという結果に。
    とはいえ、これもこの時点での結果。  
    手順やルールを覚えてもライブラリ側のアプデで陳腐化する可能性があるので、必ず「自分で、最新で、定期的に」検証するようにしたい。
