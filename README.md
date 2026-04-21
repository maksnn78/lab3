# Лабораторная работа №3
## Аксентьев Макисм ИУ8-22
## Подготовка
```bash
git clone https://github.com/tp-labs/lab03 tmp
git clone https://github.com/maksnn78/lab3.git
cd lab3
cp -r ../tmp/* .
rm -rf ../tmp
echo "" > README.md
```
## Задание 1
```bash
cd formatter_lib

cat > CMakeLists.txt <<EOF
cmake_minimum_required(VERSION 3.4)
project(formatter)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_library(formatter STATIC formatter.cpp)
target_include_directories(formatter PUBLIC \${CMAKE_CURRENT_SOURCE_DIR})
EOF

cd ..
```
## Задание 2
```bash
cd formatter_ex_lib

cat > CMakeLists.txt <<EOF
cmake_minimum_required(VERSION 3.4)
project(formatter_ex)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_library(formatter_ex STATIC formatter_ex.cpp)

target_include_directories(formatter_ex PUBLIC \${CMAKE_CURRENT_SOURCE_DIR})

target_link_libraries(formatter_ex PUBLIC formatter)
EOF

cd ..
```
## Задание 3
### Создание hello_world_application
```bash
cd hello_world_application

cat > CMakeLists.txt <<EOF
cmake_minimum_required(VERSION 3.4)
project(hello_world_application)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_executable(hello_world_application hello_world.cpp)

target_link_libraries(hello_world_application formatter_ex)
EOF

cd ..
```
### Создание solver_application
```bash
cd solver_application

cat > CMakeLists.txt <<EOF
cmake_minimum_required(VERSION 3.4)
project(solver_application)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_executable(solver_application equation.cpp)

target_link_libraries(solver_application formatter_ex solver_lib)

target_include_directories(solver_application PUBLIC
${CMAKE_SOURCE_DIR}/solver_lib)
EOF

cd ..
```
### Сборка и демонстрация работы
```bash
cat > CMakeLists.txt <<EOF
cmake_minimum_required(VERSION 3.4)
project(lab3)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_subdirectory(formatter_lib)
add_subdirectory(formatter_ex_lib)
add_subdirectory(solver_lib)
add_subdirectory(hello_world_application)
add_subdirectory(solver_application)
EOF
```
```bash
vboxuser@Ubuntu1:~/lab3$ cmake -H. -B_build
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- The C compiler identification is GNU 13.3.0
-- The CXX compiler identification is GNU 13.3.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
CMake Deprecation Warning at formatter_lib/CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


CMake Deprecation Warning at formatter_ex_lib/CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


CMake Deprecation Warning at solver_lib/CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


CMake Deprecation Warning at hello_world_application/CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


CMake Deprecation Warning at solver_application/CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- Configuring done (1.0s)
-- Generating done (0.0s)
-- Build files have been written to: /home/vboxuser/lab3/_build
```
```bash
vboxuser@Ubuntu1:~/lab3$ cmake --build _build
[ 20%] Built target formatter
[ 40%] Built target formatter_ex
[ 50%] Building CXX object solver_lib/CMakeFiles/solver_lib.dir/solver.cpp.o
[ 60%] Linking CXX static library libsolver_lib.a
[ 60%] Built target solver_lib
[ 70%] Building CXX object hello_world_application/CMakeFiles/hello_world_application.dir/hello_world.cpp.o
[ 80%] Linking CXX executable hello_world_application
[ 80%] Built target hello_world_application
[ 90%] Building CXX object solver_application/CMakeFiles/solver_application.dir/equation.cpp.o
[100%] Linking CXX executable solver_application
[100%] Built target solver_application
```
```bash
vboxuser@Ubuntu1:~/lab3$ ./_build/hello_world_application/hello_world_application
-------------------------
hello, world!
-------------------------
```
```bash
vboxuser@Ubuntu1:~/lab3$ ./_build/solver_application/solver_application
1 5 6
-------------------------
x1 = -3.000000
-------------------------
-------------------------
x2 = -2.000000
-------------------------
```
## Отправка на github
```bash
rm -rf _build
git add .
git status
```
```bash
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   CMakeLists.txt
	new file:   LICENSE
	new file:   README.md
	new file:   formatter_ex_lib/CMakeLists.txt
	new file:   formatter_ex_lib/formatter_ex.cpp
	new file:   formatter_ex_lib/formatter_ex.h
	new file:   formatter_lib/CMakeLists.txt
	new file:   formatter_lib/formatter.cpp
	new file:   formatter_lib/formatter.h
	new file:   hello_world_application/CMakeLists.txt
	new file:   hello_world_application/hello_world.cpp
	new file:   preview.png
	new file:   solver_application/CMakeLists.txt
	new file:   solver_application/equation.cpp
	new file:   solver_lib/CMakeLists.txt
	new file:   solver_lib/solver.cpp
	new file:   solver_lib/solver.h
```
```bash
git commit -m "Lab3: CMake build system with libraries and applications"
```
```bash
[main (root-commit) 5cc89d6] Lab3: CMake build system with libraries and applications
 17 files changed, 549 insertions(+)
 create mode 100644 CMakeLists.txt
 create mode 100644 LICENSE
 create mode 100644 README.md
 create mode 100644 formatter_ex_lib/CMakeLists.txt
 create mode 100644 formatter_ex_lib/formatter_ex.cpp
 create mode 100644 formatter_ex_lib/formatter_ex.h
 create mode 100644 formatter_lib/CMakeLists.txt
 create mode 100644 formatter_lib/formatter.cpp
 create mode 100644 formatter_lib/formatter.h
 create mode 100644 hello_world_application/CMakeLists.txt
 create mode 100644 hello_world_application/hello_world.cpp
 create mode 100644 preview.png
 create mode 100644 solver_application/CMakeLists.txt
 create mode 100644 solver_application/equation.cpp
 create mode 100644 solver_lib/CMakeLists.txt
 create mode 100644 solver_lib/solver.cpp
 create mode 100644 solver_lib/solver.h
```
```bash
git push -u origin main
```
```bash
Username for 'https://github.com': maksnn78
Password for 'https://maksnn78@github.com': 
Enumerating objects: 24, done.
Counting objects: 100% (24/24), done.
Delta compression using up to 4 threads
Compressing objects: 100% (24/24), done.
Writing objects: 100% (24/24), 1.01 MiB | 5.68 MiB/s, done.
Total 24 (delta 3), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (3/3), done.
To https://github.com/maksnn78/lab3.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main'.
```
