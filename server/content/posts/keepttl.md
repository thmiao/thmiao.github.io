---
title: "关于go-redis与KeepTTL"
date: 2021-12-22T09:12:33+08:00
draft: false
tags : [
    "golang",
    "redis"
]
---

​		Redis在6.0版本之后增加了SET命令的KEEPTTL选项保留该键的生存时间，但是go-redis只在注释里备注了，没有做校验或向下兼容，如果对应的redis服务器版本小于6.0直接使用-1作为失效时间则会直接收到错误。

```go
// Set Redis `SET key value [expiration]` command.
// Use expiration for `SETEX`-like behavior.
//
// Zero expiration means the key has no expiration time.
// KeepTTL is a Redis KEEPTTL option to keep existing TTL, it requires your redis-server version >= 6.0,
// otherwise you will receive an error: (error) ERR syntax error.
func (c cmdable) Set(ctx context.Context, key string, value interface{}, expiration time.Duration) *StatusCmd {
	args := make([]interface{}, 3, 5)
	args[0] = "set"
	args[1] = key
	args[2] = value
	if expiration > 0 {
		if usePrecise(expiration) {
			args = append(args, "px", formatMs(ctx, expiration))
		} else {
			args = append(args, "ex", formatSec(ctx, expiration))
		}
	} else if expiration == KeepTTL {
		args = append(args, "keepttl")
	}

	cmd := NewStatusCmd(ctx, args...)
	_ = c(ctx, cmd)
	return cmd
}
```

如果要用这个功能建议还是进行升级，或者在使用go-redis前计算剩余时间作为ttl
