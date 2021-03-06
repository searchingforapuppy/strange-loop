---
title: "JavaScript questions"
created: "2021-09-25"
updated: "2021-10-31"
---

## 概要

[javascript-questions](https://github.com/lydiahallie/javascript-questions)の深掘りしたいトピック

## Q1,Q2

var と let の違いについての問題。

| items         | const           | let             | var       |
| :------------ | :-------------- | :-------------- | :-------- |
| redeclaration | no              | no              | yes       |
| reassignment  | no              | yes             | yes       |
| scope         | block           | block           | function  |
| hoisting      | reference error | reference error | undefined |

Q1 は hoisting に関連する問題。「宣言なくして初期化なし」が let と const の特徴である。

Q2 は JS の実行モデルが関わってくるのでややこしいが、要するに関数スコープとブロックスコープの違いを問うている。

下のスクリプトにおいて、test1()の var で宣言された変数 x は、関数内で有効なので 1 を出力するが、test2()の let で宣言された変数 x は、{}内でのみ有効なので console.log(x)はエラーとなる。

```JavaScript
function test1() {
  if (true) {
    var x = 1;
  }

  console.log(x);
}

function test2() {
  if (true) {
    let x = 1;
  }
  console.log(x);
}

test1();
test2();
```

## Q3

ordinary function と arrow function の違い。
arrow function は this との結びつきを持たないので、たとえば shape 内に`thisRad: () => this.radius`というメソッドを定義し、それを呼び出した場合、this.radius はオブジェクト内の radius を参照せず、undefined が返ってくる。

[アロー関数の概要](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

## Q5

ブラケット記法とドット記法の違いに関する問題。
ドットの後に続くプロパティが、その実態は string であるのは考えてみると初学者にとってはややこしい。

[JavaScript Quickie— Dot Notation vs. Bracket Notation](https://codeburst.io/javascript-quickie-dot-notation-vs-bracket-notation-333641c0f781)

## Q6

JS において、あるオブジェクトに他のオブジェクトを代入する場合、参照渡しになるという例。両者ともに同じメモリを参照しているので、一方で値を変更したら、他方の値呼び出し結果も変わる。

プリミティブ型の変数に関しては、値渡しが適用される。

[データ型一覧](https://developer.mozilla.org/ja/docs/Web/JavaScript/Data_structures)

[値渡しと参照渡し](https://qiita.com/migi/items/3417c2de685c368faab1)

## Q8

クラスからインスタンスを new 演算子で生成した時、クラスで static に定義されたメソッドの扱いがどうなるのか、という問題。

new 演算子は組み込みやユーザ定義のクラス(より正確にはオブジェクト型)から、メソッドやプロパティを継承したインスタンスを生成する機能である。

ただし、クラスにおいて、static で定義されたメソッドやプロパティは、new で生成したインスタンスに渡されない

この問題では、最後の行の`console.log(freddie.colorChange('orange'));`によって、インスタンスには継承されない static なメソッドである colorChange にアクセスしようとしているので、エラーになる。

freddie インスタンスが colorChange を継承していないのは、`"colorChange" in freddie`の返り値が undefined になることによっても確かめられる

[new 演算子](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Operators/new)

## Q11

プロパティやメソッドのプロトタイプ継承についての問題。これまで、prototype の仕様について、よく理解しないまま書いてきたので、この問題は学習のよいきっかけになった。

[MDN の記事](https://developer.mozilla.org/ja/docs/Web/JavaScript/Inheritance_and_the_prototype_chain#using_prototypes_in_javascript)によると、オブジェクトのメソッドにアクセスした場合、prototype をどんどんさかのぼっていき、それ以上先の prototype がない場合(null を返す場合)に、undefined を返すというメカニズムらしい。

この問題の場合、Person へのメソッド追加に prototype がないため、子オブジェクトには追加されたメソッドが継承されない。
そのことは、`"getFullName" in member`が false を返すことで確かめられる。

<!--
- オブジェクトの継承元を特定する
  - Object.getPrototypeOf(obj)
  - obj.\_\_proto\_\_\
- オブジェクトのプロパティを列挙する
  - Object.getPropertyNames(obj)
- オブジェクトのメソッドを列挙する
- オブジェクトがあるプロパティを持つかどうかを確認する
  - property in obj
    - 継承元まで含めてチェックする
  - Object.getOwnProperty(obj)
    - 継承元はチェックしない
- オブジェクトの継承元を変更する
  - Object.getPrototypeOf(obj)
 -->

## Q12

new キーワードの有無で、インスタンスの挙動がどう変わるのかを問う問題。new なしだと、this のコンテクストはグローバルオブジェクトを参照する。

```JavaScript
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

const lydia = new Person("Lydia", "Hallie");
const sarah = Person("Sarah", "Smith");

console.log(lydia);
console.log(global.firstName);
console.log(global.lastName);
console.log(sarah);
```

## Q16

postfix な incremental 演算子と、 prefix な incremental 演算子の違いを問う問題。普段は postfix なバージョンを使うので、後者を使うべき場面というのが思いつかないな。。

## Q17

タグ付きテンプレートリテラルの挙動の問題。

- テンプレートリテラルの特徴
  - ソースの中に挿入された改行文字は、すべてテンプレートリテラルの一部になる(\n がいらない)
  - 本問のように、関数名+テンプレートリテラル文字列の組み合わせをタグ付きテンプレートリテラルとよび、関数の最初の引数が文字列の配列となり、残りの引数が式に渡される

[テンプレートリテラル (テンプレート文字列)](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Template_literals)

## Q18

==と\===の違いを問う問題。型変換した結果での等値性を調べる必要がある場面はほぼないので、\===をいつも使っている。あとは Object.is()も等値性比較に使えるが、これでないといけない場面はまだ出会ったことがない。Jest や Chai などのユニットテストライブラリの内部実装とかで使われているんだろうか？

[等価性の比較と同一性](https://developer.mozilla.org/ja/docs/Web/JavaScript/Equality_comparisons_and_sameness)

## Q19

Rest parameters(残余引数)についての問題。Rest parameters は、不定数の引数を配列として関数に渡し、処理するために使われる。同様の使い方をするための仕組みとして、ES6 以前は arguments オブジェクトが使われていた。両者の違いは、それが配列であるか否かである。

```JavaScript
function getAge(...args) {
  // typeofでは同様の値を表示するが
  console.log(typeof arguments);
  console.log(typeof args);

  // argumentsは配列ではない
  console.log(Array.isArray(args));
  console.log(Array.isArray(arguments));
  console.log(Array.isArray(Array.from(arguments)));
}

getAge(21);
```

[残余引数](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Functions/rest_parameters)

<!-- TODO TypeScriptで残余引数を使う場合の型指定の方法について書く -->

## Q20

Strict モードの挙動に関する問題。Strict モードで変更される挙動は多岐に渡るが、大雑把にまとめると、次のような特徴がある。

- JavaScript モジュールでインポートされたモジュールは自動的に Strict モードになる
- 過去に宣言のなかったグローバル変数への代入は ReferenceError になる
- 通常のモードでは暗黙に失敗するミス（主に代入に関連するもの）を、例外を発生させるエラーとして扱う
- eval や arguments など、扱いの難しい関数の機能や影響範囲を制限する
- 将来の ECMAScript で導入される可能性のある予約語を、変数や引数の名前として使えなくする

<!-- ## Q21

名前解決の問題
eval()の回避策 -->

## Q22

JS の Storage API についての問題。
セッションストレージのデータは、ブラウザのタブが閉じられるときに消去されるが、ローカルストレージは明示的に削除されない限り、保存され続ける。これは、サーバにストレージの情報が保存されていて、ブラウザが再接続するときにそこから http ヘッダでストレージ情報を受け取るということなのだろうか？
<https://developer.mozilla.org/ja/docs/Web/API/Storage>

Storage API は一見便利そうだけれども、[この記事](https://www.rdegges.com/2018/please-stop-using-local-storage/)をみると、ごく簡単でユーザ登録が不要なアプリを除き、使用は避けた方が良さそう。

## Q25

重複する key がオブジェクトに存在する場合、対応する値には何が選ばれるか、という問題で、最後に追加された値が選ばれる。これは多くの場合、同様の値が存在することを知らずに追加してしまうというケースだと予想されるので、避けたい挙動のはず。TypeScript を導入するしかエラー検知の方法はないのか？

<!-- TODO TypeScriptを使った上書き回避策か、JSでの回避策を書く -->

## Q29

オブジェクトの key を文字列に変換するとき、その key が\[object Object\]になってしまうという奇妙な挙動を取り上げた問題。これは一体なぜ？

## Q33

this が指すコンテクストに対して何らかの操作を施す call や bind の特徴を問う問題。

```JavaScript
const person = { name: "Lydia" };

function sayHi(age) {
  return `${this.name} is ${age}`;
}


console.log(sayHi.call(person, 21));

// bindを挟むことで、関数の実行タイミングを遅らせることができる
console.log(sayHi.bind(person, 21).call());
console.log(sayHi.bind(person, 21).apply());
```

```JavaScript
const numbers = [5, 6, 2, 3, 7];

// applyとcallの違い
console.log(Math.max.apply(null, numbers));
console.log(Math.max.call(null, 5, 6, 2, 3, 7));
```

### Q35

if 文や三項演算子の条件節の真偽判定において、false となる値、すなわち falsy values は何かという問題。これは暗記するか、すぐに参照できるようにしておきたい知識である。

### Q40

reduce()の挙動を問う問題。reduce()は非常に便利な関数だけれども、渡せる引数の数や形式のオプションが多く、それぞれ挙動も異なってくるので注意深く使う必要がある。

例(
<https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce>のコードを編集)：

```JavaScript
const getMax = (a, b) => Math.max(a, b);

/*
init: 50
arr[0] -> 1 -> getMax(50, 1) -> 50
arr[1] -> 100 -> getMax(50, 100) -> 100
*/
console.log([1, 100].reduce(getMax, 50)); // 100

/*
init: 10
arr[0] -> 50 -> getMax(10, 50) -> 50
*/
console.log([50].reduce(getMax, 10)); // 50

/*
init: empty -> arr[0] -> 1
arr[1] -> getMax(1, 100) -> 100
*/
console.log([1, 100].reduce(getMax)); // 100

/*
init: empty -> arr[0] -> 50
callback is not called
*/
console.log([50].reduce(getMax)); // 50

/*
init: 1
callback is not called
 */
console.log([].reduce(getMax, 1)); // 1

// TypeError
console.log([].reduce(getMax));
```

<!-- TODO deep dive to reduce -->

<!-- ### Q44 -->

<!-- <https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Iterators_and_Generators> -->

<!-- TODO deep dive to generator -->

### Q45

<https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Iterators_and_Generators>

### Q46

<!-- 超重要！！ -->

## Q68

```JavaScript
console.log(new Number(2) === new Number(2));
console.log(new Boolean(false) === new Boolean(false));
console.log(new Symbol("foo") === new Symbol("foo"));
```

<!-- Number()と Boolean()は、new 演算子なしだとプリミティブを生成する関数なのかな？ -->
