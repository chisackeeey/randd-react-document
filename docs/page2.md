# 2. React とは

## 概要

- JavaScript の View ライブラリの一つ
  - `Facebook` が開発
  - `Yahoo!`や `Airbnb` など多くの企業で採用されている
  - UI 開発に特化している
  - `JSX`という JavaScript の拡張言語を採用している

### JSX とは

- JSX とは React の UI を html ライクに記述するためのライブラリ

  - React では以下の様にコンポーネントを作成する

  ```js
  const Hello = () => (
  React.createElement('div', null, [
    React.createElement('h1', { className: 'hello-world' }, 'Hello World'),
    React.createElement('p', { id: 'hello' }, 'Hello Hello Hello!'),
  ]);
  );
  ```

  - JSX を用いると同じコンポーネントを以下の様に作成することができる

  ```js
  const Hello = () => (
    <div>
      <h1 className="hello-world">Hello World</h1>;
      <p id="hello">Hello Hello Hello!</p>
    </div>
  );
  ```

  - 実際には内部的に上の例と同じ様に変換されている
  - html ライクな形式を用いることでより直感的で見慣れた形式で記述することができる

## React のコンセプト

- [公式サイト](https://ja.reactjs.org/)では以下の 3 点がコンセプトとして掲げられている

### Declarative(宣言的である)

- `React` はあるべき姿を宣言的に記述し、状態が更新されるとそれに合わせて全体を再描画する
- コードが読みやすく、デバッグが容易である

  ```jsx
  function ClickMe() {
    // state = 状態の宣言
    const [message, setMessage] = useState("Click me!");

    // クリック時の挙動を定義
    const onClick = () => setMessage("Clicked!");

    render() {
      // 宣言的に記述する。state が更新されると自動的に再描画する。
      return (
        <div>
          <p onClick={onClick}>{message}</p>
        </div>
      );
    }
  }
  ReactDOM.render(<ClickMe />, document.body);
  ```

### Component-Based(コンポーネント指向である)

- `React` はコンポーネント指向のライブラリである
- カプセル化されたコンポーネント(部品)の集合によってアプリケーションを構成する

```jsx
// Menuコンポーネント
function Menu() {
  return <h1>This is Menu</h1>;
}

// Contentコンポーネント
function Content({ title }) {
  return <p>Today Content is {title}</p>;
}

// 上記2つのコンポーネントを使用している
function App() {
  return (
    <div>
      <Menu />
      <Content title="React" />
    </div>
  );
}

ReactDOM.render(<App />, document.getElementById("root"));
```

### Learn Once, Write Anywhere(一度の学習で何度でも書ける)

- `React` の知識は `ios` や `android` 等の Web 以外のプラットフォームにも適用することができる
- 例えば、モバイルアプリ開発では `React Native` という `React` の概念を基盤としたフレームワークを用いる
- Web で html タグを使っている部分をプラットフォームに応じたタグに変えるだけで開発できる

## React で用いる JavaScript の基本文法

### 変数の宣言

- 変数を定義する際に `const` もしくは `let` を宣言する
- Java とは違って明確に型を宣言することは無い

```jsx
const name = "hirai";
let age = 24;
```

#### const

- `const` で宣言した変数は再代入ができない(Java でいう final 変数)

```jsx
const name = "hirai";
name = "ozaki"; // エラー
```

#### let

- `let` で宣言した変数は再代入が可能

```jsx
let name = "hirai";
name = "ozaki"; // エラーにならない
```

#### 使い分け

- 基本的には `const`で宣言する
- 再代入が必要な場合に限り`let`で宣言する

### 関数

- `function` を使った書き方と`アロー関数`を使った書き方がある

#### function を使った書き方

- 基本形は以下の通り

```jsx
function 関数名(引数) {
  // 処理
  return 戻り値;
}
```

- Java のように戻り値やアクセス修飾子を明示するようなことはしない

```jsx
// 関数の定義
function add(x, y) {
  return x + y;
}

// 関数を呼び出す
add(1, 2); // 3
```

- 関数を変数に格納することもできる

```jsx
// 関数の定義
const add = function add(x, y) {
  return x + y;
};

// 変数に入れた場合も同じように呼び出せる
add(1, 2); // 3
```

- 関数を変数に格納することもできる

```jsx
// 関数の定義
const add = function add(x, y) {
  return x + y;
};

// 変数に入れた場合も同じように呼び出せる
add(1, 2); // 3
```

- 変数に入れる場合は`function`の後ろの関数名を省略しても同様の動きとなる

```jsx
// 関数の定義
const add = function(x, y) {
  return x + y;
};

// 変数に入れた場合も同じように呼び出せる
add(1, 2); // 3
```

#### アロー関数

- `function`というキーワードを省略した新しい書き方
- 基本形は以下の通り

```jsx
const 関数名 = (引数) => {
  // 処理
  return 戻り値;
};
```

- これまでの足し算の関数は以下のように書ける

```jsx
// 関数の定義
const add = (x, y) => {
  return x + y;
};

// 関数を呼び出す
add(1, 2); // 3
```

- 処理が一行だけの場合や丸括弧をつける場合は以下のように`return`を省略して書くこともできる

```jsx
// 処理が一行だけの場合
const add = (x, y) => x + y;

// 丸括弧をつける場合
const multiply = (x, y) => (
  x * y;
);

// 関数を呼び出す
add(1, 2); // 3
multiply(1, 2); // 2
```

- 引数が 1 つの場合は()を省略できる

```jsx
// 関数の定義
const hello = (name) => {
  console.log(`Hello ${name}`);
};

// 関数を呼び出す
hello("hirai"); // Hello hirai
```

#### 使い分け

- モダンな記法では基本的にアロー関数を使っておけば問題ない
- [参考リンク](https://qiita.com/ozaki25/items/0a428dc3ac31a116576a)

### 配列の操作

#### 配列の宣言

- `[]`で囲うことで配列を宣言することができる

```jsx
const months = ["April", "May", "June"];
const list = ["文字列", 100, true]; // 複数の型のデータを混在させることもできる
```

#### ループ処理

##### forEach

- 配列の各要素に対して単純な繰り返し処理をする場合は`forEach`を使う

```jsx
const months = ["April", "May", "June"];

months.forEach((month) => {
  console.log(month);
});

// April
// May
// June
```

##### map

- 配列の各要素に対して処理を行い、新しい配列を生成する場合は`map`を使う

```jsx
const numbers = [1, 2, 3];

const newNumbers = numbers.map((num) => {
  return num * 10;
});

console.log(newNumbers);

// [10, 20, 30]
```

#### 配列の結合

- 複数の配列を結合する書き方

```jsx
const array1 = [1, 2];
const array2 = [4, 5];

const newArray = [...array1, ...array2];

console.log(newArray);
// [1, 2, 4, 5]
```

- 以下のようにして配列に値を追加することもできる

```jsx
const array1 = [1, 2];
const array2 = [4, 5];

const newArray = [0, ...array1, 3, ...array2, 6];

console.log(newArray);
// [0, 1, 2, 3, 4, 5, 6]
```

### オブジェクトの操作

- key/value 形式の配列のようなもの

#### オブジェクトの宣言

- `{}`の中に`key: value`の形式で記述するとオブジェクトを宣言できる

```jsx
const user1 = { name: "hirai" };

// カンマ区切りで複数の値を設定できる
const user2 = { name: "hirai", age: 24, height: "173cm" };
```

#### オブジェクトの使い方

##### 値を取得する

- 以下の 2 パターンどちらでも可能

```jsx
const user = { name: "hirai", age: 24 };
const name = user.name; // 取り出し方1
const age = user["age"]; // 取り出し方2

console.log(name); // hirai
console.log(age); // 24
```

- 以下の様に省略することも可能

```jsx
const user = { name: "hirai", age: 24 };
const { name, age } = user;

console.log(name); // hirai
console.log(age); // 24
```

##### 値を追加する

- 取得と同様に 2 パターンある

```jsx
// 空っぽのオブジェクト
const user = {};
user.name = "hirai"; // 追加の仕方1
user["age"] = 24; // 追加の仕方2

console.log(user); // {name: "hirai", age: 24}
```

- 変数の宣言時に定義することも可能

```jsx
const user = { name: "hirai", age: 24 };

console.log(user); // {name: "hirai", age: 24}
```

- オブジェクトの key 名と代入する変数名が同じ場合、以下の様に省略することも可能

```jsx
const name = "hirai";
const age = 24;
// const user = { name: name, age: age } と同じ意味
const user = { name, age };

console.log(user); // {name: "hirai", age: 24}
```

### 三項演算子

- 三項演算子は if 文を省略して書く記法

```jsx
条件式 ? trueの場合の処理 : falseの場合の処理;
```

- 通常の if 文は以下

```jsx
const age = 24;
let message;

if (age >= 18) {
  message = "You can vote!"; // trueの場合
} else {
  message = "You can't vote!"; // falseの場合
}
```

- 三項演算子を使うと以下の様に書ける

```jsx
const age = 24;
const message = age >= 18 ? "You can vote!" : "You can't vote!";
```

### import と export

- React では様々なライブラリやモジュールをインポートする

```jsx
// ライブラリやモジュールからのインポート
import React from "react"; // ファイルごとインポート
import { Button, Table } from "react-bootstrap"; // 任意のコンポーネントを指定してインポート

// 自分で作成したファイルからのインポート
import Menu from "src/components/Menu"; // ファイルのパスを指定
```

- 作成したファイルを他のファイルからインポートするためには、ファイル内でエクスポートする必要がある

```jsx
function App() {
  ...
}

export default App;
```

```

```
