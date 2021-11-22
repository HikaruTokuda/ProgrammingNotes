# C# Tips

C#にはこれまで習得した内容以外にも様々な機能がある。  
それらを順に紹介する。  

## 標準ライブラリ  

ライブラリとは、それ自体はアプリケーションではないが、別のアプリケーションに組み込むことで様々な機能を提供してくれるプロジェクトを指す。  

<br>

### 文字列の操作  

string型は様々な機能を提供してくれる。  

#### 文字列の長さを取得する  

```CSharp
var str = "string length";
int length = str.Length;
```  

<br>

#### 文字列を大文字、半角全角、ひらがなカタカナを区別せずに比較する  

「==」演算子で文字列を比較した場合は、いずれも大文字/小文字を区別して文字列を比較する。もしも、大文字/小文字を区別しないで比較するならば、以下のようにする。  

```CSharp
var str1 = "wings";
var str2 = "WINGS";
str1.Equals(str2, StringComparison.OrdinalIgnoreCase);  // true or false
string.Compare(str1, str2, StringComparison.OrdinalIgnoreCase); //str1 > str2であれば正数、str1 = str2であれば0、str1 < str2であれば負の数が返る
```  
半角/全角、ひらがな/カタカナを区別しないで比較したい場合は、CompareInfoクラスのCompareメソッドを使用する。CompareOptions.IgnoreWidthで全角/半角の違いを、CompareOptions.IgnoreKanaTypeでひらがな/カタカナの違いを無視して比較できる。  

<br>

```CSharp
using System.Globalization;

var full = "ＷＩＮＧＳ";
var half = "WINGS";

var ci = CultureInfo.CurrentCulture.CompareInfo;    // 現在の地域情報に基づいて(OSの地域情報)文字列の比較ルールを取得

ci.Compare(full, half); // 結果：1(異なる)
ci.Compare(full, half, CompareOptions.IgnoreWidth); // 結果： 0(等しい)
```