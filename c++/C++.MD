* 音乐

  * 头文件

    ```c++
     #include <mmsystem.h>
    ```

  * 加载静态库

    ```c++
    #pragma comment(lib,"winmm.lib")
    ```

  * 打开音乐

    ```c++
    mciSendString("open 音乐路径 alias mucis",0,0,0)
    音乐路径:
    ```

  * 播放音乐

    ```c++
    mciSendString("play music repeat",0,0,0)
    ```

* 星空(Easyx图形库)  需要安装图形库

  * 头文件

    ```c++
     #include <graphics.h>
    ```

  * 创建图形窗口

    ```c++
    initgraph(int width, int height)
    ```

  * 画点

    ```c++
    putpixel(int x, int y, color)
    ```

* 流星图片输出(贴图) 批量输出

  * 设置图片变量

    ```c++
    IMAGE img
    ```

  * 加载图片

    ```c++
    loadimage(&img, "图片路径.jpg",400,400)
    ```

  * 输出图片

    ```c++
    putimage(0,0,&img)
    ```

* 随机函数

  * 头文件

    ```
    time.h
    ```

  * 随机函数种子

    ```c++
    srand((unsigned)time(NULL))
    ```

  * rand随机取值

  * 结构体

    ```c++
    定义结构体
    struct 结构体名 {
    	数据成员
    }
    
    输出结构体
    结构体名.数据成员名
    ```
