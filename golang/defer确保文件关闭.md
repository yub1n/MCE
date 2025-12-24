![image-20251224232510316](./../_resources/image-20251224232510316.png)

在最后再关闭很容易忘记

![image-20251224232534141](./../_resources/image-20251224232534141.png)

再看看go怎么读取一个文件

假设有这样的文本文件

![image-20251224232619025](./../_resources/image-20251224232619025.png)

![image-20251224232907799](./../_resources/image-20251224232907799.png)

查看Read文档，n int没有用，直接用

结果是

![image-20251224232933462](./../_resources/image-20251224232933462.png)

![image-20251224232952789](./../_resources/image-20251224232952789.png)

![image-20251224233023817](./../_resources/image-20251224233023817.png)

说明这个n还是有用的，是实际的字节数

![image-20251224233111474](./../_resources/image-20251224233111474.png)

ai说这样处理文件有更大的问题，题外话：这个路径前面其实可以省略

![image-20251224233211883](./../_resources/image-20251224233211883.png)

验证一下

搞一个大于1024字节的文本，随便copy一个内置函数源码

![image-20251224233614163](./../_resources/image-20251224233614163.png)

结果

![image-20251224233656420](./../_resources/image-20251224233656420.png)

真的只有前面1024个字节

循环读取

```go
package main

import (
	"fmt"
	"io"
	"os"
)

func ReadFile(path string) error {
	file, err := os.Open(path)
	if err != nil {
		return err
	}
	defer file.Close()
	for {
		buf := make([]byte, 1024)
		n, err := file.Read(buf)
		if n > 0 {
			fmt.Print(string(buf[:n]))
		}
		if err != nil {
			if err == io.EOF {
				break
			}
			return err
		}
	}
	return nil
}

func main() {
	err := ReadFile("text.txt")
	if err != nil {
		fmt.Println(err)
	}
}

```

![image-20251225004535561](./../_resources/image-20251225004535561.png)

![image-20251225004550303](./../_resources/image-20251225004550303.png)