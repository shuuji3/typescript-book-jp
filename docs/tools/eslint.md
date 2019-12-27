# ESLint

ESLintはJavaScriptのlintを行うためのソフトウェアです。しかし、現在では[TypeScript](https://github.com/Microsoft/TypeScript/issues/29288)のデファクトのlinterとなっています。[2つの開発チームの協力](https://eslint.org/blog/2019/01/future-typescript-eslint)に感謝しましょう。

## インストール

ESLintをTypeScript向けにセットアップするには、以下のパッケージが必要です。

```sh
npm i eslint eslint-plugin-react @typescript-eslint/parser @typescript-eslint/eslint-plugin
```

> ヒント: ESLintでは、lintのルールが含まれるパッケージを"plugin"と呼びます。

* eslint : コアのeslintパッケージ
* eslint-plugin-react : ESLintが提供するReactのためのルールセット。[サポートするルールの一覧](https://github.com/yannickcr/eslint-plugin-react#list-of-supported-rules)
* @typescript-eslint/parse : ESLintがts/tsxファイルをパースして解釈できるようにするパッケージ。
* @typescript-eslint/eslint-plugin : TypeScript用のルールセット。[サポートするルールの一覧](https://github.com/typescript-eslint/typescript-eslint/tree/master/packages/eslint-plugin#supported-rules)

> 2つのESLintパッケージ(jsとts向け)と2つの@typescript-eslintパッケージ(ts向け)があるだけなので、TypeScriptのオーバーヘッドは*それほど大きくは*ありません

## 設定

`.eslintrc.js`を次の内容で作成します。

```js
module.exports = {
  parser: '@typescript-eslint/parser',
  parserOptions: {
    project: './tsconfig.json',
  },
  plugins: ['@typescript-eslint'],
  extends: [
    'plugin:react/recommended',
    'plugin:@typescript-eslint/recommended',
  ],
  rules:  {
    // Overwrite rules specified from the extended configs e.g.
    // "@typescript-eslint/explicit-function-return-type": "off",
  }
}
```

## 実行

あなたのプロジェクトの`package.json`に次のような`scripts`を追加します。

```json
{
  "scripts": {
    "lint": "eslint \"src/**\""
  }
}
```

これで、`npm run lint`コマンドを実行することでESLintによる検証が実行できるようになりました。

## VSCodeの設定

* ESLint用の拡張機能をインストールします。 https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint
* `settings.json`に次の設定を追加します。

```js
"eslint.validate":  [
  "javascript",
  "javascriptreact",
  {"language":  "typescript",  "autoFix":  true  },
  {"language":  "typescriptreact",  "autoFix":  true  }
],
```
