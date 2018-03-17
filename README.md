# nanogui GLES wasm
**what is it** this if fork of [nanogui](https://github.com/wjakob/nanogui) modified for WASM and GLES (*nanovg* and *nanogui* source files modified)

**live demo** [link](https://danilw.github.io/GLSL-howto/nanogui/nanogui.html)

# Building

```sh
$ cd ext
$ git clone https://github.com/libigl/eigen.git
$ cd ..
$ em++ -DNANOVG_GLES3_IMPLEMENTATION -DGLFW_INCLUDE_ES3 -DGLFW_INCLUDE_GLEXT -DNANOGUI_LINUX -Iext/nanovg/ ext/nanovg.c --std=c++11 -O3 -lGL -lGLU -lm -lGLEW -s USE_GLFW=3 -s FULL_ES3=1 -s USE_WEBGL2=1 -o nanovg.bc
$ em++ -DNANOVG_GLES3_IMPLEMENTATION -DGLFW_INCLUDE_ES3 -DGLFW_INCLUDE_GLEXT -DNANOGUI_LINUX -Iinclude/ -Iext/nanovg/ -Iext/eigen/ button.cpp checkbox.cpp colorpicker.cpp colorwheel.cpp combobox.cpp common.cpp glcanvas.cpp glutil.cpp graph.cpp imagepanel.cpp imageview.cpp label.cpp layout.cpp messagedialog.cpp popup.cpp popupbutton.cpp progressbar.cpp screen.cpp serializer.cpp slider.cpp stackedwidget.cpp tabheader.cpp tabwidget.cpp textbox.cpp theme.cpp vscrollpanel.cpp widget.cpp window.cpp nanogui_resources.cpp nanovg.bc --std=c++11 -O3 -lGL -lGLU -lm -lGLEW -s USE_GLFW=3 -s FULL_ES3=1 -s USE_WEBGL2=1 -s WASM=1 -o nanogui.bc
$ mkdir build
$ em++ -DNANOVG_GLES3_IMPLEMENTATION -DGLFW_INCLUDE_ES3 -DGLFW_INCLUDE_GLEXT -DNANOGUI_LINUX -Iinclude/ -Iext/nanovg/ -Iext/eigen/ nanogui.bc example1.cpp --std=c++11 -O3 -lGL -lGLU -lm -lGLEW -s USE_GLFW=3 -s FULL_ES3=1 -s USE_WEBGL2=1 -s WASM=1 -o build/nanogui.html --preload-file ./icons
```

**Problems**
 - std::thread (pthread) support in wasm disabled [check this](https://www.mail-archive.com/emscripten-discuss@googlegroups.com/msg07008.html)
 - asserts in wasm does not fit C asserts
 - glGetError() has too much errors, better skip checking
 - exceptions to build with -s DISABLE_EXCEPTION_CATCHING=2

**pthread** *nanogui can be builded in wasm with pthreads -s USE_PTHREADS=2 -s PTHREAD_POOL_SIZE=10
need to remove while(true) loop from threads (common.cpp line 79) 
building with pthread give you (much)less FPS and 100% processor usage, to launch it you need use old browser like firefox 57*
