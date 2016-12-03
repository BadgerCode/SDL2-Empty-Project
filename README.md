### A sample, empty C++ project for Visual Studio 2015 (VS2015) with SDL2 ###
This has been tested in VS2015 Update 3.

Extra libaries **not** included:
* SDL Image: https://www.libsdl.org/projects/SDL_image/
* SDL Fonts: https://www.libsdl.org/projects/SDL_ttf/
* SDL Networking: https://www.libsdl.org/projects/SDL_net/

To add these libraries:
* Download the files
* Add the include files to solution_dir/include/SDL2
* Add the lib files to solution_dir/lib
* Add the lib files to the project settings (Linker -> Input -> Additional Dependencies)
* Add the dll files to your output directory debug/release folder(s)

----

### Setting up SDL project in visual studio 2015. ###

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

#### 8. Build it. 
There shouldn't be any errors.<br>
**Do not run it yet though**

#### 9. Copy solution_dir/lib/SDL2.dll to your output directory
* If you didn't do the previous step, the output directory will be solution_dir/
* **You need to put it in the debug subfolder**.
* If you build in release mode later on, you will have to put it into the release subfolder too.

#### 10. Run it
There shouldn't be any errors.<br>
When you run it, a black console window will pop up and then close.
