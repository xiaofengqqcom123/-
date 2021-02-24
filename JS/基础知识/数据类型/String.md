### String
字符串的内部格式始终是 UTF-16，它不依赖于页面编码

#### 1. 字符串类型转换：
- alert value: 将 value 转换为字符串类型，然后显示这个值
- String(value) : 将 value 转换为字符串类型
- 隐私转换：
```
// 二元 + 是唯一一个以这种方式支持字符串的运算符。其他算术运算符只对数字起作用，并且总是将其运算元转换为数字。
alert( '1' + 2 ); // "12"
alert( 2 + '1' ); // "21"
alert(2 + 2 + '1' ); // "41"，不是 "221"
```

#### 2. 转义字符
\u{X…XXXXXX} （1 到 6 个十六进制字符）
具有给定 UTF-32 编码的 unicode 符号。一些罕见的字符用两个 unicode 符号编码，占用 4 个字节。这样我们就可以插入长代码了。
```
alert( "\u00A9" ); // ©
alert( "\u{20331}" ); // 佫，罕见的中国象形文字（长 unicode）
alert( "\u{1F60D}" ); // 😍，笑脸符号（另一个长 unicode)
```

#### 3. 访问字符
- 使用方括号 [pos]
- 调用 str.charAt(pos) 方法

它们之间的唯一区别是，如果没有找到字符，[] 返回 undefined，而 charAt 返回一个空字符串：
```
let str = `Hello`;

alert( str[1000] ); // undefined
alert( str.charAt(1000) ); // ''（空字符串）
```

#### 4. 获取子字符串
JavaScript 中有三种获取字符串的方法：substring、substr 和 slice。
```
// slice
"hello".slice(1, 2) // e
"hello".slice(-2, -1) // l
"hello".slice(2, 1) // ""

// substring
"hello".substring(1, 2) // e
"hello".substring(2, 1) // e
"hello".substring(-2, -1) // ""

// substr
"hello".substr(1, 4) // ello 其中 4 代表长度
"hello".substr(-2, 1) // s
```

#### 5. 比较大小
```
alert( 'a' > 'Z' ); // true
alert( 'Österreich' > 'Zealand' ); // true

// codePointAt
alert( "z".codePointAt(0) ); // 122

// formCodePoint
alert( String.fromCodePoint(90) ); // Z

// 常见英文字母
let str = '';

for (let i = 65; i <= 220; i++) {
  str += String.fromCodePoint(i);
}
"ABCDEFGHIJKLMNOPQRSTUVWXYZ[\]^_`abcdefghijklmnopqrstuvwxyz{|}~ ¡¢£¤¥¦§¨©ª«¬­®¯°±²³´µ¶·¸¹º»¼½¾¿ÀÁÂÃÄÅÆÇÈÉÊËÌÍÎÏÐÑÒÓÔÕÖ×ØÙÚÛÜ"

alert( 'Österreich'.localeCompare('Zealand') ); // -1
```


#### 6.变音符号与规范化
在许多语言中，都有一些由基本字符组成的符号. 例如字母 a 可以是 àáâäãåā 的基本字符。但不是全部，因为可能的组合太多。于是支持任意组合
```
“dot above” 字符（代码 \u0307）
“dot below”（代码 \u0323）
```