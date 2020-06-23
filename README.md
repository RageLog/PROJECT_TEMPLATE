# PROJECT_TEMPLATE

PROJECT_TEMPLATE is a C++ cmake project template. If you ask to me "Why is that .zip file", I say that "Because, it is contain YOUR_PROJECT_NAME project file git inited with first "Project created !" commit add "0.0.0.0" tag. When I try to upload "PROJECT_TEMPLATE" folder with underfolder. This project work with FOLDER NAME and It is important for me.". If you want to create project or library with little or nothing changes in CMake files, don't think twice about using this (Of course think this but I won't :D). I'm using clang 10, ninja and VS Code with cmake tool on Windows. I cannot try to another platform. I could try out to this with GCC 10.1.0, clang 10.0.0 MSVC 2019 tool but MSVC give error with shared library because unfortunately I'm not define SHARED_EXPORD header now. Other compiler is generate .a file instead of .lib in windows. I will fix that.

This template is create for to provide to as that:
(at least my goal is that :D)

* Simple project creatation
* Fast development and fast sub folder generation
* Easily pipelined development with cmake in C++(or C)
* Ease use
* Automatic version import in your main code.
* Serve many option.
* Clang formating almost automatic each source file
* Packagin almost automatic with CPack(I know that, this is CMake feature but you wont write any code for this)
* Ease testing with googletest
* Ready usage with vcpgk (maybe! I don't know.  I try this only once :/. Least issue is with msvc compiler. I will fix this. I hope :D)



## How to use

Firstly, I'm going to explain the project structure. I build on classic project structere(generally). The structure is:

        |YOUR_PROJECT_NAME
        |
        ||---->| apps
        |      |
        |      |----> CMakeLists.txt
        |      |----> main.cpp
        |
        ||---->| cmake
        |      |
        |      |----> ClangFormat.cmake
        |      |----> util.cmake
        |      |----> VersionFromGit.cmake
        |      |---->     ...
        |
        ||---->| external_libs
        |      |
        |      |----> googletest
        |      |---->     ...
        |      |----> CMakeLists.txt
        |
        ||---->| include
        |      ||---->| YOUR_PROJECT_NAME
        |      |      ||---->| YOUR_LIBRARY_NAME
        |      |      |      |      |---->Your_header.h
        |      |      |      |---->     ...
        |      |      |
        |      |      ||---->     ...
        |
        ||---->| resources
        |      |----> YOUR_PROJECT_NAME.ico
        |      |---->     ...
        |
        ||---->| src
        |      ||---->| YOUR_LIBRARY_NAME
        |      |      |     |---->Your_header.cpp
        |      |      |     |---->     ...
        |      |      |     |---->CMakeLists.txt
        |      |      |
        |      |      |---->     ...
        |      |      |---->CMakeLists.txt
        |      |      |---->ver.h.in
        |
        ||---->| tests
        |      ||---->| YOUR_TEST_NAME
        |      |      |     |---->YOUR_TEST_NAME.cpp
        |      |      |     |---->     ...
        |      |      |     |---->CMakeLists.txt
        |      |      |---->     ...
        |      |      |---->CMakeLists.txt
        ||----> .clang-format
        ||----> .clang-format-ignore
        ||----> .gitignore
        ||----> CMakeLists.txt
        ||----> LICENCE.md
        ||----> README.md

I have some rules for this template usage. If in this table are there any folder have same name another folder or file , you must be make same whole of them. 

## Usage steps

1.  * Change YOUR_PROJECT_NAME foler name. 
    * This will your project name and you will generate package and exe file with this name. 
    * if you change this, you must change the "include->YOUR_PROJECT_NAME" and the "resources->YOUR_PROJECT_NAME.ico".

2.  * if you want create new library, only copy and paste YOUR_LIBRARY_NAME folder in src and  include-> YOUR_PROJECT_NAME.
    * And then change its name. 
    * This will provide to you generate automatically library this name.
    * This library will link automatically
    * cpp file must be inside of src->YOUR_LIBRARY_NAME
    * hpp or h file must be inside of include->YOUR_PROJECT_NAME->YOUR_LIBRARY_NAME
    * Repeat this steps how many you want.

3.  * For test, again copy and paste YOUR_TEST_NAME file how many you want.
    * Change the .cpp file name it have same name with folder. I mean, if your folder name is tester_1, the .cpp file name must be tester_1.cpp.
    * Write your test code in YOUR_TEST_NAME.cpp file.
    * Please chack out there is googletest in external library. If there is no google test folder clone that.

4.  * For clangformate,firstly, you must build(or call cmake I use cmake tool with VS code)
    * Go to the build file with cd ./build command
    * Type ninja clangformat (for me. For you what you use. For exemple make clangformat)
    * It is will.

5.  * For packeging with cpack,firstly, you must build(or call cmake I use cmake tool with VS code)
    * Go to the build file with cd ./build command
    * Type ninja package (for me. For you what you use. For exemple make package)
    * Output is in package folder with YOUR_PROJECT_NAME installer name and YOUR_PROJECT_NAME.ico icon

6.  * If you want to add external libraries without vcpkg, clone it to external lib
    * Change main CMakeLista.txt file what is necessary for this folder under #internal libs comment.

7. * If you want to add external libraries with vcpkg, You must clone vcpkg and make ready to use. You can find this on vcpkg github page.
    * Sometimes, vcpkg give to you which command must adding in your main CMakeLists. Sometimes, you also should check the vcpkg/ports/usage file. This commands is like that:
    * #find_package(SDL2 CONFIG REQUIRED) -> Before your executable(apps) or library(src) file. I put comment(# Find packages go here.) for this .
    * #target_link_libraries(HelloWorld PRIVATE SDL2::SDL2 SDL2::SDL2main) -> After your executable(apps) or library(src) file. I put comment(#vcpkg linking) for this .
    * Maybe you need to set vcpkg root directroy in main CMakeLists.txt


 ## Options

 * USE_VCPKG (default OFF) activate vcpkg usage (You must set root dir)
 * PASS_VERSION (default ON) if this is on, git tag is pass through CMake to your source code
 * USE_CUSTOM_DIR (default ON) exe and libs will out to Output folder in YOUR_PROJECT_NAME
 * BUILD_STATIC (default OFF) Set Shared or static linking. Off because I love dll :D
 * CREATE_RUNTIME_FILE (default ON) If this is off, build doesn't generate exe file. Only library mode.
 * ADD_TO_PACKAGE_LIB_HEADER (default ON) Sometimes, maybe,you want genarete packages with libs and header(such as vulkan sdk :D), sometimes don't.
 * USE_NSIS (default ON) packaging with NSIS or zip 
 * USE_ICON (default ON) Using packaging icone from resources
 * ENABLE_TESTING (default ON) Test enabling
 * ENABLE_clangformat (default ON) Activate clangformat.

