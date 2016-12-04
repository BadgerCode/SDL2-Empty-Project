# A sample, empty C++ project for Visual Studio 2015 (VS2015) with SDL2 #
This has been tested in VS2015 Update 3.

[Getting Started with SDL2](http://headerphile.com/)

### Extra Libraries
These have **not** been included in this project.

* SDL Image: https://www.libsdl.org/projects/SDL_image/
* SDL Fonts: https://www.libsdl.org/projects/SDL_ttf/
* SDL Networking: https://www.libsdl.org/projects/SDL_net/

To add these libraries:
* Download the files
* Add the include files to **solution_dir/include/SDL2** _(they must be in the same folder as the other SDL2 files)_
* Add the lib files to **solution_dir/lib** _(including the dlls)_
* Add the lib file names to the project settings (**Linker -> Input -> Additional Dependencies**) _(SDL2file.lib;...)_
* Add the dll files to your output directory debug/release folder(s) _(unless you set up Visual Studio to copy the dlls on build)_


### How to rename this project after cloning it
Replace **NewName** with the project name you want.

* Empty.sln -> **NewName**.sln
  * Edit the file and change line 6 from ```"Empty", "Empty\Empty.vcxproj"``` to ```"NewName", "NewName\NewName.vcxproj"```
* Empty/ -> **NewName**
* Empty/Empty.vcxproj -> **NewName**/**NewName**.vcxproj
  * Edit the file and change line 23 from ```<RootNamespace>Empty</RootNamespace>``` to ```<RootNamespace>NewName</RootNamespace>```
* Empty/Empty.vcxproj.filters -> **NewName**/**NewName**.vcxproj.filters
* Empty/Empty.vcxproj.user -> **NewName**/**NewName**.vcxproj.user

----

# Setting up SDL project in visual studio 2015. #

* FOLLOW THESE STEPS EXACTLY.<br>
* At any point during these steps, building might result in an error:	**"entry point must be defined"**.<br>
* You must do all of the steps before building &amp; running will work.<br>
* **solution_dir** is your the location of your solution.
* If you follow this guide, but get a linker error in VS2015 (e.g. entry point must be defined), you may need to [follow this guide](http://headerphile.com/sdl2/sdl2-part-0-setting-up-visual-studio-for-sdl2/).


#### 1. Create a new project (empty visual c++ project)
Create a new source file called "main.cpp"

#### 2. Download SDL2
* https://www.libsdl.org/download-2.0.php
* SDL2-devel-2.?.?-VC.zip (Visual C++ 32/64-bit)

#### 3. At the top level of your solution, make three folders:
1. include
2. include/SDL2
3. lib

#### 4. In the SDL zip download, copy the following
1.  include/* to solution_dir/include/SDL2
2.  lib/x86/* to solution_dir/lib<br>
**Use x64 at your own risk!**

#### 5. In visual studio, right click on the project (not solution) and click properties
##### 5.1. C/C++: General
1. Edit Additional Include Directories
2. Set it to $(SolutionDir)include

##### 5.2. Linker: General
1. Edit Additional Libary Directories
2. Set it to $(SolutionDir)lib

##### 5.3. Linker: Input
1. Edit Additional Dependencies
2. Enter: SDL2.lib and SDL2main.lib on separate lines

##### 5.4. Linker: System
Set SubSystem to Console

#### 6. [Optional] Change output directory
1. Go to the project properties again
2. Click on General
3. Set Output Directory to $(ProjectDir)\bin\$(Configuration)\

#### 7. Main.cpp- Add the following code
```c++
#include "SDL2/sdl.h"

int main(int argc, char** argv)
{
	SDL_Init(SDL_INIT_EVERYTHING);
	return 0;
}
```
_SDL2 needs your main to have the above, non-typical format because SDL2 will call it from its main._

#### 8. Make Visual Studio copy the .dll files to the output directory after building
1. Go to the project properties again
2. Go to Build Events -> Post-Build Event
3. Set the **Command Line** to ```xcopy /d /y "$(SolutionDir)lib\*.dll" "$(OutDir)"```
4. Set the **Description** to ```Copies required dlls```

#### 9. Remove the option to build for x64
You won't be able to build in 64-bit unless you also set up the 64-bit files for SDL2.

1. Go to the project properties again
2. Click **Configuration Manager** in the top-right
3. Click on the **Active solution platform** dropdown and click **Edit**
4. Remove the x64 option

#### 10. Build & run it. 
There shouldn't be any errors.<br>
When you run it, a black console window will pop up and then close.
