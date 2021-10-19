# Fudamental of C# programming

## 変数  

<br>

### 変数の宣言

変数は、値を保存しておく場所。  
変数を使うには、***宣言***しなければならない。  
C#で変数を宣言されたら、コンピュータは変数に値が入る前からその変数に必要なメモリを確保する。  

```CSharp
データ型 変数名 (= 初期値);
```

データ型とは変数に格納できる値の種類を表す情報。  
例えば、以下のような変数の宣言を書いたとする。  

```CSharp
int data;
```

intは整数型と言って、int型で宣言された変数には整数値しか格納できない。  

変数の宣言は、以下のようにまとめることもできる。  

```CSharp
int data1, data2;
```

この場合、data1、data2ともにint型として宣言されている。  

また、変数には宣言と同時に初期値を格納する事もできる。  

```CSharp
int data = 1;
data = 2;
```

この場合、宣言時はdataには1が格納されているが、data = 2;を実行した時点でdataに格納されている値は2に書き換えられる。  

<br>

### 変数の名前のつけ方  

変数の名前のつけ方については、C#の開発元であるMicrosoftが定義している。  
[C# コーディングルール](https://docs.microsoft.com/ja-jp/dotnet/csharp/fundamentals/coding-style/coding-conventions)  

ただし、簡単には以下のような感じで覚えておけば良い。  

- 1文字目はアルファベットまたはアンダーコアであること
- 2文字目以降は、1文字目で使える文字、もしくは数字であること
- 変数名に含まれるアルファベットの大文字/小文字は区別される
- 予約語でないこと  

予約語とは、C#としてあらかじめ意味が決められた単語である。  

[C# 予約語](https://ufcpp.net/study/csharp/ap_reserved.html)  

変数の名前は厳密には以下のようなルールがある。  
[識別子　記法](https://qiita.com/munieru_jp/items/c150f5e8865d5c075d37)  

### 定数  

変数と定数の違いは、宣言後に変更できるかどうか。  

```CSharp
const データ型 定数名 = 値;
```  

変数の場合は、宣言後に値を変更できる。  

```CSharp
string data = "initial value";
data = "second value";
```

これはＯＫ。  
ただし、定数の場合は宣言後に値を変更できない。

```CSharp
const string data = "initial value";
data = "second value";  // ←エラー
```  

定数は、変更させたくない値を保持する場合などに有効活用できる。  
例えば、アプリケーションが外部サイトのＵＲＬを参照している場合、どこかで誰かが変更したら、参照先を書き換えられたら困る。  

<br>

## データ型  

上述のデータ型をもう少し詳しく見てみる。  

<br>

### データ型の分類

[データ型一覧](https://dianxnao.com/c_sharp%E3%83%87%E3%83%BC%E3%82%BF%E5%9E%8B%E4%B8%80%E8%A6%A7/)  

<br>

### 整数型

int

整数型は符号の有無(マイナス値を含むかどうか)、格納できる値の範囲によって以下のように分類される。  

[整数型](https://docs.microsoft.com/ja-jp/dotnet/csharp/language-reference/builtin-types/integral-numeric-types)  

***特別な理由がない場合は、int型を使う***

```CSharp
int data = 1;
```

<br>

### 浮動小数点数  

double, float

浮動小数点型は、小数を格納するデータ型である。  
[浮動小数点型](https://docs.microsoft.com/ja-jp/dotnet/csharp/language-reference/builtin-types/floating-point-numeric-types)  

2進数で浮動小数点数を表現するには、以下のようなルールに従っている。  
[浮動小数点数の作り方](https://yossan.hatenablog.com/entry/2021/01/02/122011)  

```CSharp
double data = 2.5;
```

<br>

### 文字型  

char型

文字型は単一の文字を保持するための型。  
char型を使用する。ただし、char型は文字を文字として保持しているわけではなく、文字として指定された値を***Unicode***として保持している。  

[Unicode](http://www.tamasoft.co.jp/en/general-info/unicode.html)  

```CSharp
char data = 'あ';
```

<br>

### 真偽値

bool型  

true(真)、false(偽)のどちらかを格納する型。  

```CSharp
bool data = true;
```

<br>

### オブジェクト型  

object型  

なんでも格納できる型。  
複雑なプログラムになると、用意した時点でどんな型の値が入るかわからない場合がある。  
そのような場合はオブジェクト型を使用する。  

```CSharp
object data1 = 1;
object data2 = 'あ';
object data3 = false;
```  

<br>

### 型推論

変数を宣言する際に、varキーワードを使うことで型の記述を省略できる。  

```CSharp
var data1 = 1;
var data2 = 'あ';
var data3 = false;
```

varキーワードで宣言した場合は、コンパイラが型を推論して勝手に型をつけてくれる。  
つまり型を明記していないだけで、以下のようなコードはコンパイルエラーになる。  

```CSharp
var data = 1;
data = 'あ';    // エラー
```

varキーワードを使って宣言する場合はいくつかの制約がある。  

- 初期値は省略できない。
- 複数の変数をまとめて宣言できない。
- フィールド宣言(後述)できない。
- varという名前のクラス(後述)があった場合はそちらを優先。  

## リテラル  

リテラルとは、データ型に格納できる値そのもの、また、値の表現方法のこと。  

<br>

### 文字列リテラル  

文字で表現しつつも、特別な意味を持つものがある。  
たとえば、改行を示す際は、「\n」と記述する。  
つまり、  

```
あしたは、
あめ。
```

と表示させたい場合などは、  

```
"あしたは、\nあめ。"
```

と記述する。  
このような表現方法は***エスケープシーケンス***などと呼ばれる。  

[エスケープシーケンスについて](https://atmarkit.itmedia.co.jp/ait/articles/1709/27/news017.html)  

