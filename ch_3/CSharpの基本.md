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

***テスト***  

- 整数型で初期化した変数の3倍の値を表示するプログラム。  

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

### 文字列への変数展開  

$"..."の形式で文字列リテラルを表すこともできる。この場合、文字列に埋め込まれた{...}の部分が、式と解釈され、その結果が文字列に埋め込まれる。  
例えば以下のような場合は、  

```CSharp
string name  = "山田";
string addedName = $"こんにちは、{name}さん。";
```  

変数addedNameには、"こんにちは、山田さん"という文字列が代入されている。  

<br>

***テスト***  

```
名前と職業を入力して、  
こんにちは、私の名前は○○です。  
職業は××です。  
```  

と表示するプログラム。  

## 型変換  

C#で宣言した型は、後から別の型の値を入力できない。  
例えば以下のようなコードはエラーになる。  

```CSharp
int data = 7;
data = "aaa";   // int型の変数に対して文字列型を代入しようとしているのでエラー
```  

そのため、一度宣言した変数のデータ型を別のデータ型として扱いたい場合は、型変換を行う必要がある。  

### 暗黙的な型変換  

数値型で、範囲のせまい型から、範囲の広い型への変換はプログラム内で明示しなくても暗黙的に型変換できる。  

```CSharp
int num = 2147483647;
long bigNum = num;
```  

[詳細](https://docs.microsoft.com/ja-jp/dotnet/csharp/programming-guide/types/casting-and-type-conversions)  

<br>

### 明示的な型変換(キャスト)  

逆に、広い型から狭い方への変換は、内容に関わらずエラーになる。  

```CSharp
int i = 13;
byte b = i; // int型の方が広範囲を処理するデータ型なのでエラー
```  

ただし、実際の値が範囲ないにあることが明らかな場合に限ってキャストが許される。  
キャストの記述は、  
```CSharp
(データ型) 変数
```

例えば、

```CSharp
int i = 13;
byte b = (byte)i;
```

### 文字列⇔数字の型変換  

文字列と数値の型変換を自分で実装しようとするのは大変である。  
文字列として入力されたものに対して、文字コードからその文字列がどの数値を表しているのかを見つけてくる必要があるからである。  
そこで、整数型や文字列型には、数値⇔文字列を変換してくれる関数(後述)があらかじめ用意されている。  
※関数が何かはともかく、ここは形で覚えてしまう。  

<br>

まずは、文字列を数値に変換する方法

```CSharp
string strNum = "10";   // 10という文字列
int num = Int32.Parse(strNum);  // 10という数値
```  

次に、数値を文字列に変換する方法  

```CSharp
int num = 20;   // 20という数値
string strNum = num.toString(); //20という文字列
```  

<br>

***テスト***  
名前と年齢を入力すると、年齢の値が3倍されて以下のように出力されるプログラム。  

```CSharp
こんにちは、○○さん(入力値の3倍の値)!
```  

<br>

## クラス型    

クラスについては後述。  
いまは、クラス型というものがあることだけ知っておけばOK。  

## null値  

nullは、何も入っていない状態を指す。  
例えば、初期化せずに宣言された変数は、値が代入されるまでnull値である。  
また変数に後から値が入る事を前提に、明示的にnull値で初期化する場合もある。  
null値のまま変数を使用しようとするとエラーになる。  
この場合、コンパイルエラーにはならず、実行されたときに初めてエラーになるので厄介。  

```CSharp
string str;
Console.WriteLine(str);     // 実行時にエラーになる。  
```  

以下のプログラムを実行し、原因を突き止める。  

```CSharp
string firstInputValue = null;
Console.WriteLine("Input value.");
firstInputValue = Console.ReadLine();

string SecondInputValue = null;
Console.WriteLine("Input value again.");
firstInputValue = Console.ReadLine();

Console.WriteLine($"あなたが1回目に入力した文字数は、{firstInputValue.Length}文字です。");
Console.WriteLine($"あなたが2回目に入力した文字数は、{SecondInputValue.Length}文字です。");
```  

## 配列型  

int, double, stringなどの型はいずれも、一度に１つの値を持つ。しかし、処理によっては、複数の値をまとめて扱いたくなるケースもよくある。  
たとえば、次にしめすのは、書籍タイトルを管理する例である。  

```CSharp
var title1 = "HTML5とApache Cordovaで始めるハイブリッドアプリ開発";
var title2 = "デザインサンプルで学ぶCSSによる実践スタイリング入門";
var title3 = "Angularアプリケーションプログラミング";
```  

title1, title2,...と通し番号がついてるので、見た目にはデータをまとめて管理しているように見える。しかし、C#からすれば、これらは何の関係もない独立した変数である。  
たとえば、本の冊数をしりたいと思ってっもすぐにカウントすることはできないし、全ての書籍タイトルを列挙したいと思っても変数をここに並べるしか術がない。  
そこで登場するのが***配列***である。  
配列は以下のように使う。  

### 配列の宣言  

#### 配列のサイズだけを宣言  

配列のサイズ(=いくつの要素を格納できるか)だけを宣言しておくやり方。  

```CSharp
データ型[] 配列名 = new データ型[要素数];
```

例：

```CSharp
int[] data = new int[5];
```  

この例では、int型の値を5つ格納できる配列"data"を宣言した。  

#### 初期値を指定した宣言  

配列型でも、初期化と宣言をまとめて記述できる。  

```CSharp
データ型[] 配列名 = {要素1, 要素2, ....};
```

例：  

```CSharp
int[] data = {1, 2, 3, 4, 5};
```  

この例では、1から5までの要素で初期化された配列"data"を宣言した。  

#### varを用いた宣言  

varを使って配列を宣言することもできる。  

```CSharp
var 変数名 = new[] {要素1, 要素2, ...};
```  

例：  

```CSharp
var data1 = new[] {1, 2, 3, 4, 5};
var data2 = new[] {"A", "B", "C", "D"};
```  

この例では、data1はint[]型、data2はstring[]型として型推論される。  

### 配列へのアクセス  

上記のように宣言した配列には、以下のようにブラケット構文([...])でアクセスできる。  

```CSharp
int data0 = data[0];
```

ブラケットでくくられた部分は、***インデックス番号***または、***添え字***と言い、配列の何番目の要素を取り出すのかを表す。インデックス番号は***0から始まる***ので、例えば要素数が5の配列で利用できるインデックス番号は0～4となる。  
配列サイズを超えたインデックス番号を指定した場合は、アプリケーションがクラッシュするので注意。  

配列の要素数を知りたい場合は、以下で求められる。  

```CSharp
int sizeOfArray = data.Length;
int maxIndex = sizeOfArray - 1;
```  

ブラケット構文を利用することで、要素の値を書き換えることもできる。  

```CSharp
int[] data = {1, 2, 3, 4, 5};   // この時点で、dataの中身は{1, 2, 3, 4, 5}
data[2] = 25;                   // dataの中身が{1, 2, 25, 4, 5}に書き換えられる
```  

ただし、要素を後から追加することはできないので注意。  

```CSharp
int[] data = new int[5];    // int型の値が5つ格納できる配列を宣言
data[5] = 6;                // ERROR: 配列の要素が1つ増えるわけではない。
```

## いろいろな配列(参考)  

[多次元配列](https://ufcpp.net/study/csharp/st_array.html)  

[ジャグ配列](https://www.wareko.jp/blog/c-sharp-jagged-array-perfect-master)  

***テスト***  
1. 次のコードは、定数を使って値引き率10%を定義し、元の値である500円の支払額を求めるコードです。空欄を埋めてコードを完成させてください。  

```CSharp
(①) double Discount = (②);
int price = 500;
double sum = price * Discount;
Console.WriteLine((③)"値引き後の価格は(④)円です。");
// 実行結果：値引き後の値は450円です。
```  

2. 以下は、あるクラスの名簿である。  

| 出席番号   |     名前      |
| --- | ----------- |
| 1    | 山田太郎 |
| 2    | 高木次郎 |
| 3    | 鈴木三郎 |
| 4    | 田中花子 |
| 5    | 石田森子 |

このクラスの人数と出席番号3番の生徒の名前を表示するプログラム。  
ただし、名簿は配列として管理し、以下のような文字列で表示させる。  

```CSharp
クラスの生徒数： ✕人
出席番号3番： ○○さん
```  
