# `hangprofile` example — پروفایل هنگی (dual profile)

The whole job is ONE library call. The example only parses flags and
prints the result; every hard part (tolerant upload, the simultaneous
dual bind, the clean-up that keeps exactly two avatars) lives in
`account.Account.HangiProfile`, exposed one line up as
`parsrubika.Hangi`.

```go
res, err := pr.Hangi("hangprofile", "+989123456789",
    "c0DBedk0525ec07fb54a35b01baf2303", "1.jpg", "2.jpg",
    account.WithHangiProgress(func(msg string) { fmt.Println(msg) }))
```

Run it:

```
go run . --phone +989123456789
go run . --phone +989123456789 --guid c0DBedk0525ec07fb54a35b01baf2303
```

| Flag | Meaning |
|---|---|
| `--phone` | your account (international format) — required |
| `--guid` | target group/channel GUID; empty = your own account |
| `--photo1` / `--photo2` | the two images (default `1.jpg` / `2.jpg`) |
| `--rounds` | dual-bind rounds; the default **1** is the correct value — more rounds only pile up avatar entries |
| `--clean` | delete all existing avatars before binding |
| `--session` | session file name (login reuse) |

The result reports the created avatar ids, how many leftovers were
removed and the final avatar count the server lists.
