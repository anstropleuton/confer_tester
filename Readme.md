# Confer Tester
Confer Tester is a testing framework for Anstro Pleuton's libraries and programs. This is a super simple, minimal testing framework to get the job of simple testing done.

# Features
- Assertion
- Testing function collection
- Customizable logging

# Prerequisite
- Know to program in C++
- Know to program in C++23 (optional, recommended)
- Know to use third party C++ libraries
- Know to use CMake

# Usage
If you are not Anstro Pleuton, which you probably are, here is a quick and rough guide to use my library:

 1. Setup:
    - Clone this repository.
    ```bash
    git clone https://github.com/anstropleuton/confer_tester
    cd confer_tester
    ```
 2. Dependencies
    - Close dependencies
    ```bash
    git submodule update --init --recursive
    ```
 3. Build the library:
    - Make build folder:
    ```bash
    mkdir build
    cd build
    ```
    - Build the project:
    ```bash
    cmake ..
    cmake --build .
    ```
 4. Install (optional, Unix/-like only)
    ```
    sudo cmake --install .
    ```
    Note: To uninstall, use `sudo cmake --build . --target uninstall`
 5. Set up path. You can use CMake and `add_library` to this directory to automatically set up path for compilation, or add include directory as `include` and lib directory to the build folder.
 6. Include the library to include all functionality:
    ```cpp
    #include "confer_tester.hpp"
    ```
 7. Go through [documentation](https://anstropleuton.github.io/confer_tester) (or [header files](include/confer_tester.hpp) to get a grasp on what you can do using my library. You can check out [examples source files](examples/) for more usage information.

# Documentations
Refer to the [documentation](https://anstropleuton.github.io/confer_tester) (or [header files](include/confer_tester.hpp) to get a grasp on what you can do using my library.

# Changelog
Refer to the [Changelog](Changelog.md) for info about changes in each version.

# Contributing
Check out [Guidelines](Guidelines.md) before you submit your code! Make sure to create a branch with one task with the name of the category of your task (i.e., "features/", "bugfix/", etc.) your task before you change the code.

# Credits
Thanks to [jothepro](https://github.com/jothepro) for the stylesheet [Doxygen Awesome](https://github.com/jothepro/doxygen-awesome-css) for Doxygen.
Thanks to Nuno Pinheiro (can't find link) for the background [Elarun](background.png). But I did find a [KDE store link](https://store.kde.org/p/1162360/) to the background image. I think you could consider that. If KDE developers are here, I would appreciate your help to find a proper link to the author.

# License
This project is licensed under the terms of MIT License, see [License](License.md).

# Junk folder?
That folder is where I put my useless features. Don't use them please.
