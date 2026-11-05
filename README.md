# zlib 1.2.11 on loongarch64

## 构建

    CFLAGS="-fPIC -O2" ./configure --prefix=$P --static
    make -j4 && make install

零补丁、零 loongarch 改动。产物 `installed/lib/libz.a`。

## 用途与验证

Doris BE 全量编译 / 链接时由 clucene、Arrow、libhdfs3 等间接依赖。
`$(P)/lib/libz.a` 已链接进 `doris_be`，0 undefined symbol。
注意它在 `installed/lib`，而 protobuf/brpc 等在 `installed/lib64`，链接时两个 `-L` 都要给。
