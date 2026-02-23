# JavaScript: var と let の違い

JavaScriptにおける var と let の主な違いは、「スコープ（有効範囲）」「再宣言の可否」「ホイスティング（吊り上げ）の挙動」の3点。

## 1. スコープ（有効範囲）の違い

- var: 関数スコープ。関数の外であればどこからでも参照できてしまったり、if や for のブロック { } を無視して外側に漏れ出したりする。
- let: ブロックスコープ。{ } の中だけで有効。ES6以降のJavaScriptではこちらが推奨される。

### 具体例
```javascript
// var の場合
function testVar() {
    if (true) {
        var x = "I am x";
    }
    console.log(x); // "I am x" （ブロックの外に漏れ出す）
}

// let の場合
function testLet() {
    if (true) {
        let y = "I am y";
    }
    console.log(y); // ReferenceError: y is not defined （ブロックの外からは見えない）
}
```

## 2. 再宣言の可否

- var: 同じ名前で何度でも宣言できてしまう。意図せず値を上書きしてしまうリスクがある。
- let: 同じスコープ内での再宣言はエラーになる。

### 具体例
```javascript
// var の場合
var name = "Alice";
var name = "Bob"; // 許容される（エラーにならない）
console.log(name); // "Bob"

// let の場合
let age = 25;
// let age = 30; // SyntaxError: Identifier 'age' has already been declared （エラーで防いでくれる）
```

## 3. ホイスティング

- var: 宣言より前で参照してもエラーにならず、undefined が返る（宣言だけが関数やグローバルスコープの先頭に巻き上げられる）。
- let: 宣言より前で参照するとエラーになる。

### 具体例
```javascript
// var の場合
console.log(a); // undefined （エラーにならないが挙動が不透明）
var a = 10;

// let の場合
// console.log(b); // ReferenceError: Cannot access 'b' before initialization （安全に落としてくれる）
let b = 20;
```

## どれを使うべき？

現代のJavaScript（ES6以降）では、以下の優先順位で使うのがベストプラクティス。

1. const: 基本はこれ（再代入しない定数）。
2. let: ループのカウンターなど、再代入が必要な場合のみ。
3. var: 原則使わない。
