# nanogui GLES wasm
**what is it** this is fork of [nanogui](https://github.com/wjakob/nanogui) modified for WASM and GLES (*nanovg* and *nanogui* source files modified)

**live demo** [link](https://danilw.github.io/GLSL-howto/nanogui/nanogui.html)

# Building

```sh
$ git clone https://github.com/libigl/eigen.git ext/eigen
$ make
```

**Problems**
 - *WARNING* I found problem with lambda in WASM, I think it work same way like in Java, in Java "*local variables referenced from a lambda expression must be final or effectively final*", I mean using any **setCallback** method you need make all variables Global (include object that call setCallback) or you can not call "callback" from other classes/functions (outside of creation function)
 - std::thread (pthread) support in wasm disabled [check this](https://www.mail-archive.com/emscripten-discuss@googlegroups.com/msg07008.html)
 - asserts in wasm does not fit C asserts
 - glGetError() has too much errors, better skip checking
 - exceptions to build with -s DISABLE_EXCEPTION_CATCHING=0

**pthread** *nanogui can be builded in wasm with pthreads -s USE_PTHREADS=2 -s PTHREAD_POOL_SIZE=10
need to remove while(true) loop from threads (common.cpp line 79) 
building with pthread give you (much)less FPS and 100% processor usage, to launch it you need use old browser like firefox 57*
