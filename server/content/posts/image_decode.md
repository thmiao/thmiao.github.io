---
title: "关于go image.Decode与import _"
date: 2021-12-27T15:20:21+08:00
draft: false
tags : [
    "golang"
]
---

​		最近在尝试go的image包时执行以下代码遇到了*go image: unknown format*的错误，其原因是缺少了image包相关的init导致Decode函数不知道怎么解码对应格式的文件。解决方法：用import _ "image/png"，执行该包的init()而不真的导入该包（避免报unused package问题），之后Decode函数可正常执行

```go
//go:embed gopher.png
var Gopher_png []byte


func init() {
	img, _, err := image.Decode(bytes.NewReader(gopher.Gopher_png))
	if err != nil {
		log.Fatal(err)
	}
	gopherInstance.gopherImage = ebiten.NewImageFromImage(img)
}
```

​		另外一提embed特性确实好用
