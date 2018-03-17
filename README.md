# nanogui GLES wasm
**what is it** this if fork of [nanogui](https://github.com/wjakob/nanogui) modified for WASM and GLES

**live demo** [link](https://danilw.github.io/GLSL-howto/nanogui/nanogui.html)

# Building

```sh
$ cd ext
$ git clone https://github.com/libigl/eigen.git
$ cd ..
$ em++ -DNANOVG_GLES3_IMPLEMENTATION -DGLFW_INCLUDE_ES3 -DGLFW_INCLUDE_GLEXT -DNANOGUI_LINUX -Iext/nanovg/ ext/nanovg.c --std=c++11 -O3 -lGL -lGLU -lm -lGLEW -s USE_GLFW=3 -s FULL_ES3=1 -s USE_WEBGL2=1 -o nanovg.bc
$ em++ -DNANOVG_GLES3_IMPLEMENTATION -DGLFW_INCLUDE_ES3 -DGLFW_INCLUDE_GLEXT -DNANOGUI_LINUX -Iinclude/ -Iext/nanovg/ -Iext/eigen/ button.cpp checkbox.cpp colorpicker.cpp colorwheel.cpp combobox.cpp common.cpp glcanvas.cpp glutil.cpp graph.cpp imagepanel.cpp imageview.cpp label.cpp layout.cpp messagedialog.cpp popup.cpp popupbutton.cpp progressbar.cpp screen.cpp serializer.cpp slider.cpp stackedwidget.cpp tabheader.cpp tabwidget.cpp textbox.cpp theme.cpp vscrollpanel.cpp widget.cpp window.cpp nanogui_resources.cpp nanovg.bc --std=c++11 -O3 -lGL -lGLU -lm -lGLEW -s USE_GLFW=3 -s FULL_ES3=1 -s USE_WEBGL2=1 -s WASM=1 -o nanogui.bc
$ em++ -DNANOVG_GLES3_IMPLEMENTATION -DGLFW_INCLUDE_ES3 -DGLFW_INCLUDE_GLEXT -DNANOGUI_LINUX -Iinclude/ -Iext/nanovg/ -Iext/eigen/ nanogui.bc example1.cpp --std=c++11 -O3 -lGL -lGLU -lm -lGLEW -s USE_GLFW=3 -s FULL_ES3=1 -s USE_WEBGL2=1 -s WASM=1 -o build/nanogui.html --preload-file ./icons
```
