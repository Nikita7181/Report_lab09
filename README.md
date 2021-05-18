#           **Отчет Lab07**
##                *Report*
- `Ход работы`

- Были выплнены следующие команды

![Туториал](https://github.com/Nikita7181/lab07)

```
export GITHUB_USERNAME=Nikita7181
alias gsed=sed
cd ${GITHUB_USERNAME}/workspace
pushd .
source scripts/activate
git clone https://github.com/${GITHUB_USERNAME}/lab06 projects/lab07
cd projects/lab07
git remote remove origin
git remote add origin https://github.com/${GITHUB_USERNAME}/lab07
mkdir -p cmake
wget https://raw.githubusercontent.com/cpp-pm/gate/master/cmake/HunterGate.cmake -O cmake/HunterGate.cmake
```

```
gsed -i '/cmake_minimum_required(VERSION 3.4)/a\
\
include("cmake/HunterGate.cmake")\
HunterGate(\
    URL "https://github.com/cpp-pm/hunter/archive/v0.23.251.tar.gz"\
    SHA1 "5659b15dc0884d4b03dbd95710e6a1fa0fc3258d"\
)\
' CMakeLists.txt
git rm -rf third-party/gtest
gsed -i '/set(PRINT_VERSION_STRING "v\${PRINT_VERSION}")/a\
\
hunter_add_package(GTest)\
find_package(GTest CONFIG REQUIRED)\
' CMakeLists.txt
gsed -i 's|add_subdirectory(third-party/gtest)||' CMakeLists.txt
gsed -i 's/gtest_main/GTest::main/' CMakeLists.txt
cmake -H. -B_builds -DBUILD_TESTS=ON
cmake --build _builds
cmake --build _builds --target test
ls -la $HOME/.hunter
git clone https://github.com/cpp-pm/hunter $HOME/projects/hunter
export HUNTER_ROOT=$HOME/projects/hunter
rm -rf _builds
cmake -H. -B_builds -DBUILD_TESTS=ON
cmake --build _builds
cmake --build _builds --target test
cat $HUNTER_ROOT/cmake/configs/default.cmake | grep GTest
cat $HUNTER_ROOT/cmake/projects/GTest/hunter.cmake
mkdir cmake/Hunter
cat > cmake/Hunter/config.cmake <<EOF
hunter_config(GTest VERSION 1.7.0-hunter-9)
EOF
mkdir demo
cat > demo/main.cpp <<EOF
#include <print.hpp>

#include <cstdlib>

int main(int argc, char* argv[])
{
  const char* log_path = std::getenv("LOG_PATH");
  if (log_path == nullptr)
  {
    std::cerr << "undefined environment variable: LOG_PATH" << std::endl;
    return 1;
  }
  std::string text;
  while (std::cin >> text)
  {
    std::ofstream out{log_path, std::ios_base::app};
    print(text, out);
    out << std::endl;
  }
}
EOF

gsed -i '/endif()/a\
\
add_executable(demo ${CMAKE_CURRENT_SOURCE_DIR}/demo/main.cpp)\
target_link_libraries(demo print)\
install(TARGETS demo RUNTIME DESTINATION bin)\
' CMakeLists.txt
mkdir tools
git submodule add https://github.com/ruslo/polly tools/polly
tools/polly/bin/polly.py --test
tools/polly/bin/polly.py --install
tools/polly/bin/polly.py --toolchain clang-cxx14
```


- После чего все было выгружено на Git hub

```
cd /home/nikita/Nikita7181/workspace/projects/Report_lab06
git add .
git commit -m "Complete tasks"
git push origin master
```

- Резултат выполнения команд

![](https://raw.githubusercontent.com/Nikita7181/Report_lab07/master/Screenshots/1.png)

![](https://raw.githubusercontent.com/Nikita7181/Report_lab07/master/Screenshots/2.png)

![](https://raw.githubusercontent.com/Nikita7181/Report_lab07/master/Screenshots/3.png)

![](https://raw.githubusercontent.com/Nikita7181/Report_lab07/master/Screenshots/4.png)

![](https://raw.githubusercontent.com/Nikita7181/Report_lab07/master/Screenshots/5.png)

![](https://github.com/Nikita7181/Report_lab07/blob/master/Screenshots/6.png)

![](https://github.com/Nikita7181/Report_lab07/blob/master/Screenshots/7.png)

![](https://raw.githubusercontent.com/Nikita7181/Report_lab07/master/Screenshots/8.png)

- После чего все было выгружено на Git hub

```
cd /home/nikita/Nikita7181/workspace/projects/Report_lab07
git add .
git commit -m "Complete tasks"
git push origin master
```
