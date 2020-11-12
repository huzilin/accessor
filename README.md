# accessor

一个简单的go generate工具，从go官方工具stringer修改而来，为结构体生成setter和getter。

结构体中字段首字母大写默认可读可写，小写则默认只读。

可以添加access的tag，控制访问属性r表示读，w表示写，用逗号分隔。


# 用法
go get gitee.com/dwdcth/accessor
添加 go:generate  accessor -type=Type1,Type2

```go
//go:generate  accessor -type=Foo

package foobar

type Foo struct {
	ReadWrite int  `access:"r,w"`
    Write int `access:"w"`
}

type Bar struct {
	ReadWrite int
    read int
}

```

