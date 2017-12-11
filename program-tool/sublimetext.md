# Sublime Text 使用技巧

## 乱数假文
经常要输入一些测试内容。SublimeText 对"乱数假文" lorem 有很好的支持。输入 lorem 再 tab 一下，就可以使用了

```
Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse
cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non
proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
```

## 批量插入序列号
安装 [InsertNums 插件](https://github.com/jbrooksuk/InsertNums)

在多行编辑模式下，快捷键 `CTRL+ALT N`  输入起始序号，`ENTER`。

## 排序
按F9或者选择菜单：Edit > Sort Lines，对每行文本进行排序

##查找重复行

排序好后，按Ctrl+F，调出查找面板
查找字符串：

```
^(.+)$[\r\n](^\1$[\r\n]{0, 1})+
```

注意：确保正则模式开关打开；若不可用，按Alt+R进行切换

点击 `Find`

## 删除重复行

排序好后，按Ctrl+H，调出替换面板

查找字符串：

```
^(.+)$[\r\n](^\1$[\r\n]{0, 1})+
```

注意：确保正则模式开关打开；若不可用，按Alt+R进行切换

替换字符串：

```
\1
```

点击Replace