len和cap同时都是这个数字大小，建议cap写多，避免后续超出时要重新分配内存。

那如果make不传数字呢？

make只有三种类型可以使用：

![ef3b0ad7eeacec0ba820dee337e52a3a.png](../_resources/ef3b0ad7eeacec0ba820dee337e52a3a.png)

map本身就是为不确定长度而设计的，比如接收前端部分更新的字段，接受大数据需要分析的不确定量的字典；

管道可以不传数字是因为分有缓冲和无缓冲两种。