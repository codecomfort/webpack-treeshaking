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

## 現在、modules: false は必要なさそう

- babelrc に modules: false を記述しなくても、結果は変わらなかった
  - webpack --display-used-exports のコンソール出力、bundle.js とも変わりない(普通に tree shaking されている)
