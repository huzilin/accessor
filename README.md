做了一个简单的go generate工具，从go官方工具stringer修改而来，为结构体生成setter和getter。

结构体中字段首字母大写默认可读可写，小写则默认只读。

可以添加access的tag，控制访问属性r表示读，w表示写，用逗号分隔。


# 用法
go get gitee.com/dwdcth/accessor
添加 go:generate  accessor -type=Type1,Type2

```go
//go:generate  accessor -type=Foo,Bar

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
会生成两个文件，foo_accessor.go 和 bar_accessor.go
foo_accessor.go
```go
// Code generated by "accessor -type=Foo,Bar"; DO NOT EDIT.

package foobar

func (f *Foo) SetReadWrite(param int) {
	f.ReadWrite = param
}
func (f *Foo) GetReadWrite() int {
	return f.ReadWrite
}
func (f *Foo) SetWrite(param int) {
	f.Write = param
}

```

bar_accessor.go

```go
// Code generated by "accessor -type=Foo,Bar"; DO NOT EDIT.

package foobar

func (b *Bar) GetReadWrite() int {
	return b.ReadWrite
}
func (b *Bar) SetReadWrite(param int) {
	b.ReadWrite = param
}
func (b *Bar) Getread() int {
	return b.read
}

```
