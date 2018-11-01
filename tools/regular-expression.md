# Regular expression: best way to find and replace texts

![comic](https://i.imgur.com/IgSEnxP.png)
<center>from [xkcd](https://xkcd.com/208/) </center>

## Todo

- [ ] [How Google Code Search Worked](https://swtch.com/~rsc/regexp/regexp4.html)
- [ ] [Regular Expression Matching Can Be Simple And Fast,but..](https://swtch.com/~rsc/regexp/regexp1.html)


## Example 1:
We can create a `list` in python. 

```
input: 
A
B
C

output:
"A",
"B",
"C",
```

<img src="https://media.giphy.com/media/5tdhGCNkAyHbqlxVvR/giphy.gif" alt="regular expression trick: create a list" width="400"/> 

<img src="https://i.imgur.com/J1mFmpv.png" alt="https://jex.im/regulex/" width="400"/> 


## Example 2:

```
my name is bob -> my name used to bob 

search: my name is (\w+)
replace: my name used to be $1
```

<img src="https://i.imgur.com/SAr1c3D.gif" alt="regular expression trick: create a list" width="400"/> 

## Example 3: 
![https://github.com/ziishaned/learn-regex](https://i.imgur.com/LU8YWCr.png)
![explain](https://i.imgur.com/18p2QsS.png)

## Exmaple 4: 

> Parse: username@domain.TLD (top level domain)

```
\b[\w.%+-]+@[\w.-]+\.[a-zA-Z]{2,6}\b
```

![email](https://i.imgur.com/AU252cK.png)

![visulization](https://i.imgur.com/Or3fSZr.png)

![result](https://i.imgur.com/N1zuTw5.png)

## The best place to learn  
![](https://i.imgur.com/LiBnRGT.png)

* [Python Regex Cheatsheet](https://www.debuggex.com/cheatsheet/regex/python): search what you want **just in one glance** 
* [JavaScript Regular Expression Visualizer](https://jex.im/regulex/#!flags=&re=%5E(a%7Cb)*%3F%24): Regular expresion **visulizer** 
* [Learn regex the easy way](https://github.com/ziishaned/learn-regex): learning regex the easy way 
* [regrexr](https://regexr.com/): Learn, build and **test** your Regular expression 
* [正则表达式30分钟入门教程](https://deerchao.net/tutorials/regex/regex.htm): 我读的第一篇正则表达式文章
* [二十个常用正则表达式](https://gist.github.com/willwang-x/dd7b961c2a7130b052b4fdc3f8ac6e26): 校验和提取

![cheatsheet](https://i.imgur.com/XgLoOt0.png)
