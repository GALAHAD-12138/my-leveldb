## 将LevelDB跑起来

首先将项目git下来：

```shell
git clone https://github.com/google/leveldb.git
```

但是这是不加submodle的

在编译之前，需下载googletest和benchmark。

切换到**leveldb/third_party/**目录下，

```shell
git clone https://github.com/google/googletest.git

git clone https://github.com/google/benchmark.git
```



### 开始编译

---

**p.s.**:第一次搞的话直接用VScod中的build不行，因为VScode的命令中没搞C++17之类的，用命令行比较好

切换到**leveldb/**目录下，然后执行

```text
mkdir -p build && cd build
cmake -DCMAKE_BUILD_TYPE=Release .. && cmake --build .
```

会出错，第二行应该改成

```text
cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_CXX_STANDARD=17 .. && cmake --build .
```

然后切换到`build/`中，执行官方的test文件

```shell
./leveldb_tests
```

之后可以按照大佬写的`test.sh`中的运行大佬的测试文件

```shell
cd ../build/ && make -j && cd ../tests

g++ -std=c++17 -o test test.cc ../build/libleveldb.a -I../include -pthread
./test
rm ./test
```

实际调用的可能是 **Clang** 编译器（Apple 的默认工具链），而不是 GNU GCC。这是因为 macOS 默认使用 `clang` 作为系统编译器，而 `g++` 通常会被符号链接到 `clang++`，但是Clang也不错了。



### 自己的仓库

---

```shell
git remote -v
git remote remove origin
git remote add origin git@github.com:GALAHAD-12138/my-leveldb.git
git branch -M main
git push -u origin main
```







### 开始学习

---

> 如果要用VScode调试或者build自己写的测试文件的话，得改CMake文件，这都是后话了