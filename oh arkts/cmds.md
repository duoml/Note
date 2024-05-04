[编译pgo环境搭建.md · haizaibali/OHCompilerDaily - Gitee.com](https://gitee.com/haizaibali/ohcompiler-daily/blob/master/%E7%BC%96%E8%AF%91pgo%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA.md#https://gitee.com/ark_standalone_build/docs)


release
```sh
export LD_LIBRARY_PATH=/home/duoml/src/standalone/out/x64.release/arkcompiler/ets_frontend:/home/duoml/src/standalone/out/x64.release/arkcompiler/ets_runtime:/home/duoml/src/standalone/out/x64.release/thirdparty/icu
export PATH=${PATH}:/home/duoml/src/standalone/out/x64.release/arkcompiler/ets_frontend:/home/duoml/src/standalone/out/x64.release/arkcompiler/ets_runtime:/home/duoml/src/standalone/out/x64.release/thirdparty/icu
```

```sh

es2abc basic.ts --type-extractor --module --merge-abc  --output test.abc
ark_js_vm --entry-point=test --enable-pgo-profiler=true --compiler-pgo-profiler-path=test.ap test.abc > /dev/null

ark_aot_compiler --enable-pgo-profiler=true --compiler-pgo-profiler-path=test.ap --aot-file=test --builtins-dts=/home/duoml/src/standalone/out/x64.release/obj/arkcompiler/ets_runtime/ecmascript/compiler/lib_ark_builtins.d.abc test.abc
ark_js_vm --entry-point=test --aot-file=test test.abc
```

debug
```sh
export LD_LIBRARY_PATH=/home/duoml/src/standalone/out/x64.debug/arkcompiler/ets_frontend:/home/duoml/src/standalone/out/x64.debug/arkcompiler/ets_runtime:/home/duoml/src/standalone/out/x64.debug/thirdparty/icu
export PATH=${PATH}:/home/duoml/src/standalone/out/x64.debug/arkcompiler/ets_frontend:/home/duoml/src/standalone/out/x64.debug/arkcompiler/ets_runtime:/home/duoml/src/standalone/out/x64.debug/thirdparty/icu
```

```sh
es2abc transformer_v1_node.js --type-extractor --module --merge-abc  --output test.abc
ark_js_vm --entry-point=test --enable-pgo-profiler=true --compiler-pgo-profiler-path=test.ap test.abc > /dev/null

ark_aot_compiler --enable-pgo-profiler=true --compiler-pgo-profiler-path=test.ap --aot-file=test --builtins-dts=/home/duoml/src/standalone/out/x64.debug/obj/arkcompiler/ets_runtime/ecmascript/compiler/lib_ark_builtins.d.abc test.abc
ark_js_vm --entry-point=test --aot-file=test test.abc
```

jit
```sh
ark_js_vm --entry-point=test --compiler-enable-jit-pgo=true --enable-pgo-profiler=true --compiler-enable-jit=true --compiler-target-triple=aarch64-unknown-linux-gnu test.abc
```


```
ark_js_vm --entry-point=test --compiler-enable-jit-pgo=true --enable-pgo-profiler=true --compiler-enable-jit=true --compiler-target-triple=aarch64-unknown-linux-gnu  --log-level=info test.abc
```