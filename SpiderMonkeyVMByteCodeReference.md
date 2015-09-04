# SpiderMonkey VMバイトコードリファレンス

## bindgname

```
bindgname GLOBAL_VARIABLE_NAME
```
グローバル変数 GLOBAL_VARIABLE_NAME を参照・代入のためバインドする。
グローバル変数を参照・代入する場合は、左辺の評価時にこの命令が必要。

- pop 0
- push 0

## call

```
call ARGUMENT_COUNT
```
VMスタックに積んだ関数を呼び出す。
ARGUMENT_COUNTはVMスタックに積んだ実引数の数。
関数と引数をVMスタックから消費し、
関数の返り値をVMスタックにpushする。

- pop 1 + ARGUMENT_COUNT
- push 1

## callgname

```
callgname GLOBAL_VARIABLE_NAME
```
グローバルな関数を呼び出す際、関数が格納された変数を評価するとき（引数の評価前）に必要。

- pop 0
- push 0

## callprop

```
callprop ATOM_ID
```
VMスタック先頭のオブジェクトから、プロパティATOM_IDの値（関数オブジェクト）を取得し、VMスタックに積む。
メソッドを呼び出すとき、プロパティを評価したときに必要。

- pop 1
- push 1

## false

```
false
```

値falseをVMスタックにpushする

- pop 0
- push 1

## getarg

```
getarg PARAM_INDEX
```
関数のパラメーターID "PARAM_INDEX" で指定されるパラメーターの値をVMスタックにpushする

- pop 0
- push 1

## getgname

```
getgname GLOBAL_VARIABLE_NAME
```
グローバル変数 GLOBAL_VARIABLE_NAME の値をVMスタックにpushする

- pop 0
- push 1

## getlocal

```
getlocal LVAR_INDEX
```
ローカル変数ID "LVAR_INDEX" で示されるローカル変数の値を取得し、
VMスタックにpushする。

- pop 0
- push 1

## getprop

```
getprop ATOM_ID
```
VMスタック先頭のオブジェクトから、プロパティATOM_IDの値を取得し、VMスタックにpushする。

- pop 1
- push 1

## goto

```
goto OFFSET
```
無条件ジャンプ命令。
PC (program counter) レジスターの値をOFFSETぶんだけ変化させる。

- pop 0
- push 0

## ifeq

```
ifeq OFFSET
```
条件付きジャンプ命令。
VMスタックの先頭の値が真ならば次の命令に行き、
偽ならばPC (program counter) レジスターの値をOFFSETぶんだけ変化させる。
真偽いずれでもVMスタックの値を1つ消費する。

- pop 1
- push 0

## int8

```
int8 NUMBER
```
符号付き8ビット整数値NUMBERをVMスタックにpushする。

- pop 0
- push 1

## int32

```
int32 NUMBER
```
符号付き32ビット整数値NUMBERをVMスタックにpushする。

- pop 0
- push 1

## uint16

```
uint16 NUMBER
```
符号なし16ビット整数値NUMBERをVMスタックにpushする。

- pop 0
- push 1

## uint24

```
uint24 NUMBER
```
符号なし24ビット整数値NUMBERをVMスタックにpushする。

- pop 0
- push 1

## neg

```
neg
```
VMスタック先頭の値の正負を反転させる。

- pop 1
- push 1

## new

```
new PARAM_COUNT
```
new式を実行しオブジェクトを生成する。PARAM_COUNTはVMスタックに積んだ引数の数。
VMスタックが以下のようなレイアウトであることを想定している（1が先頭側）。

1. ……
2. 引数2
3. 引数1
4. レシーバー

レシーバーまでがVMスタックからpopされ、新しく生成されたオブジェクトをVMスタックにpushする。

- pop 1 + (引数の数)
- push 1

## null

```
null
```
JavaScriptのnull値をVMスタックにpushする。

- pop 0
- push 1

## pop

```
pop
```
VMスタック先頭の値をpopする。

- pop 1
- push 0

## popv

```
popv
```
VMスタック先頭の値をpopし、現在実行中のスクリプトの返り値としてセットする。

- pop 1
- push 0

## push

```
push
```
VMスタック先頭の値をもう1つpushする。いわゆるdup操作。

- pop 0
- push 1

## return

```
return
```
VMスタック先頭の値をpopし、現在実行中の関数の返り値としてセットする。
関数の実行を中断する。

- pop 1
- push 0

## setarg

```
setarg PARAM_INDEX
```
現在の関数のパラメーターID "PARAM_INDEX" で示されるパラメーターに、
VMスタック先頭の値をセットする。VMスタックの値は消費しない。

- pop 0
- push 0

## setgname

```
setgname GLOBAL_VARIABLE_NAME
```
グローバル変数 GLOBAL_VARIABLE_NAME にVMスタック先頭の値を代入する。

- pop 0
- push 0

## setlocal

```
setlocal LOCAL_VARIABLE_ID
```
ローカル変数ID "LOCAL_VARIABLE_ID" で示されるローカル変数にVMスタック先頭の値を代入する。

- pop 0
- push 0

## setprop

```
setprop ATOM_ID
```
オブジェクトの、ATOM_IDで示されるプロパティに値をセットする。
スタックが以下のレイアウトであることを想定している（1が先頭側）。

1. 値
2. オブジェクト

VMスタックから値を2つpopし、値を再pushする。

- pop 2
- push 1

## stop

```
stop
```
関数またはスクリプトの実行を停止させる。
すべての関数・スクリプトのバイトコードの末尾に必要（SpiderMonkeyの最適化の都合）。

- pop 0
- push 0

## string

```
string ATOM_ID
```
文字列リテラルをVMスタックにpushする。

- pop 0
- push 1

## this

```
this
```
現在実行中のコンテキストにおけるthisの値をVMスタックにpushする。

- pop 0
- push 1

## true

```
true
```
JavaScriptのtrueの値をVMスタックにpushする。

- pop 0
- push 1