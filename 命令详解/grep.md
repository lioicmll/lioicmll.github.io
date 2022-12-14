## 1. grep

> grep 指令用于查找内容包含指定的范本样式的文件，如果发现某文件的内容符合所指定的范本样式，预设 grep 指令会把含有范本样式的那一列显示出来。若不指定任何文件名称，或是所给予的文件名为 -，则 grep 指令会从标准输入设备读取数据

## 2. 常用选项

参数 | 说明
-- | --
--color | 表示对匹配到的文本着色显示
-i | 在搜索时忽略大小写
-n | 显示结果所在的行号
-c | 统计匹配到行数，注意是行数，不是次数
-o | 只显示符合条件的字符串，但是不整行显示，每个符合条件的字符串单独显示一行
-v | 输出不带关键字的行（反向查询，反向匹配）
-w | 匹配整个单词，如果是字符串中包含这个单词，则不作匹配
-x | 整行完全匹配输出
-A| 后面都跟阿拉伯数字, 显示匹配后和它后面的n行
-B | 后面都跟阿拉伯数字, 显示匹配行和它前面的n行
-C | 后面都跟阿拉伯数字, 匹配行和它前后各n行
-e | 实现多个选项的匹配，逻辑or关系
-q | 静默模式，不输出任何信息，当我们仅关心有没有匹配到，不关心匹配到的内容时使用该命令，然后使用echo $? 查看是否匹配到，0表示匹配到，1表示没有匹配到
-P | 表示使用兼容Perl的正则引擎
-E | 使用扩展正则表达式，相当于egrep
