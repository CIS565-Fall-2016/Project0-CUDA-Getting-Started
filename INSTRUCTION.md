Project 0 CUDA Getting Started: Instructions
========================

This is due **Saturday, September 3 2016**.

**Summary:** In this project, you will set up your CUDA development tools and
verify that you can build, run, and do performance analysis.

This project is a simple program that demonstrates CUDA and OpenGL functionality
and interoperability, testing that CUDA has been properly installed. If the
machine you are working on has CUDA and OpenGL 4.0 support, then when you run
the program, you should see either one or two colors depending on your
graphics card.

This project (and all other CUDA projects in this course) requires an NVIDIA
graphics card with CUDA capability. Any card with Compute Capability 2.0
(`sm_20`) or greater will work. Gheck your GPU on this [compatibility
table](https://developer.nvidia.com/cuda-gpus).  If you do not have a personal
machine with these specs, you may use computers in the SIG Lab.

**If you need to use the lab computer for your development:**

* Thanks to Neal and @likangning93
> CUDA 7.5, Visual Studio 2010, 2013 and 2015, CMake and Git are already installed on those machines.  I’m away from the office until August 22nd. Can you test the software for us.  I can help you make adjustments and configuration changes when I return.  The software is installed on the HMS Lab PCs (stations MOR103-50 thru MOR103-57) and on all of the CETS Lab PCs including the machines in Moore 100B and Moore 100C.

* You will not presently be able to do GPU performance profiling. This will be
  very important for debugging performance bottlenecks in your program. If you
  do not have administrative access to any CUDA-capable machine, please email
  the TA.


## Part 1: Setting up your development environment

Skip this part if you are developing on a lab computer.

### Windows

1. Make sure you are running Windows 7/8/10 and that your NVIDIA drivers are
   up-to-date. You will need support for OpenGL 4.0 or better in this course.
2. Install Visual Studio 2013 (**not** 2015).
   * 2010/2012 will also work, if you already have one installed.
   * http://www.seas.upenn.edu/cets/software/msdn/
   * You need C++ support. None of the optional components are necessary.
3. Install [CUDA 7.5](https://developer.nvidia.com/cuda-downloads?sid=925343).
   * CUDA 7.5 is recommended for its new performance profiling tools.
     However, 7.0 is fine. 
   * Use the Express installation. If using Custom, make sure you select
     Nsight for Visual Studio.
4. Install [CMake](http://www.cmake.org/download/). (Windows binaries are
   under "Binary distributions.")
5. Install [Git](https://git-scm.com/download/win).

### OS X

1. Make sure you are running OS X 10.9 or newer.
2. Install XCode (available for free from the App Store).
   * On 10.10, this may not actually be necessary. Try running `gcc`
     in a terminal first.
3. Install OS X Unix Command Line Development Tools (if necessary).
4. Install [CUDA 7](https://developer.nvidia.com/cuda-downloads?sid=925343)
   (don't use cask; the CUDA cask is outdated).
   * CUDA 7.5 is recommended for its new performance profiling tools.
   * Make sure you select Nsight.
5. Install [Git](https://git-scm.com/download/mac)
   (or: `brew install git`).
6. Install [CMake](http://www.cmake.org/download/)
   (or: `brew cask install cmake`).

### Linux

Note: to debug CUDA on Linux, you will need an NVIDIA GPU with Compute
Capability 5.0.

1. Install [CUDA 7.5](https://developer.nvidia.com/cuda-downloads?sid=925343).
   * CUDA 7.5 is recommended for its new performance profiling tools.
   * Make sure you select Nsight.
2. Install Git (`apt-get install git` on Debian/Ubuntu).
3. Install CMake (`apt-get install cmake` on Debian/Ubuntu).


## Part 2: Fork & Clone

1. Use GitHub to fork this repository into your own GitHub account.
2. If you haven't used Git, you'll need to set up a few things.
   * On Windows: In order to use Git commands, you can use Git Bash. You can
     right-click in a folder and open Git Bash there.
   * On OS X/Linux: Open a terminal.
   * Configure git with some basic options by running these commands:
     * `git config --global push.default simple`
     * `git config --global user.name "YOUR NAME"`
     * `git config --global user.email "GITHUB_USER@users.noreply.github.com"`
     * (Or, you can use your own address, but remember that it will be public!)
3. Clone from GitHub onto your machine:
   * Navigate to the directory where you want to keep your 565 projects, then
     clone your fork.
     * `git clone` the clone URL from your GitHub fork homepage.

* [How to use GitHub](https://guides.github.com/activities/hello-world/)
* [How to use Git](http://git-scm.com/docs/gittutorial)


## Part 3: Build & Run

* `src/` contains the source code.
* `external/` contains the binaries and headers for GLEW and GLFW.

**CMake note:** Do not change any build settings or add any files to your
project directly (in Visual Studio, Nsight, etc.) Instead, edit the
`src/CMakeLists.txt` file. Any files you add must be added here. If you edit it,
just rebuild your VS/Nsight project to make it update itself.

### Windows

1. In Git Bash, navigate to your cloned project directory.
2. Create a `build` directory: `mkdir build`
   * (This "out-of-source" build makes it easy to delete the `build` directory
     and try again if something goes wrong with the configuration.)
3. Navigate into that directory: `cd build`
4. Open the CMake GUI to configure the project:
   * `cmake-gui ..` or `"C:\Program Files (x86)\cmake\bin\cmake-gui.exe" ..`
     * Don't forget the `..` part!
   * Make sure that the "Source" directory is like
     `.../Project0-CUDA-Getting-Started`.
   * Click *Configure*.  Select your version of Visual Studio, Win64.
     (**NOTE:** you must use Win64, as we don't provide libraries for Win32.)
   * If you see an error like `CUDA_SDK_ROOT_DIR-NOTFOUND`,
     set `CUDA_SDK_ROOT_DIR` to your CUDA install path. This will be something
     like: `C:/Program Files/NVIDIA GPU Computing Toolkit/CUDA/v7.5`
   * Click *Generate*.
5. If generation was successful, there should now be a Visual Studio solution
   (`.sln`) file in the `build` directory that you just created. Open this.
   (from the command line: `explorer *.sln`)
6. Build. (Note that there are Debug and Release configuration options.)
7. Run. Make sure you run the `cis565_` target (not `ALL_BUILD`) by
   right-clicking it and selecting "Set as StartUp Project".
   * If you have switchable graphics (NVIDIA Optimus), you may need to force
     your program to run with only the NVIDIA card. In NVIDIA Control Panel,
     under "Manage 3D Settings," set "Multi-display/Mixed GPU acceleration"
     to "Single display performance mode".

### OS X & Linux

It is recommended that you use Nsight.

1. Open Nsight. Set the workspace to the one *containing* your cloned repo.
2. *File->Import...->General->Existing Projects Into Workspace*.
   * Select the Project 0 repository as the *root directory*.
3. Select the *cis565-* project in the Project Explorer. From the *Project*
   menu, select *Build All*.
   * For later use, note that you can select various Debug and Release build
     configurations under *Project->Build Configurations->Set Active...*.
4. If you see an error like `CUDA_SDK_ROOT_DIR-NOTFOUND`:
   * In a terminal, navigate to the build directory, then run: `cmake-gui ..`
   * Set `CUDA_SDK_ROOT_DIR` to your CUDA install path.
     This will be something like: `/usr/local/cuda`
   * Click *Configure*, then *Generate*.
5. Right click and *Refresh* the project.
6. From the *Run* menu, *Run*. Select "Local C/C++ Application" and the
   `cis565_` binary.


## Part 4: Modify

1. Search the code for `TODO`: you'll find one in `src/main.cpp` on line 13.
   Change the string to your name, rebuild, and run.
   (`m_yourName = "TODO: YOUR NAME HERE";`)
2. Take a screenshot of the window (including title bar) and save it to the
   `images` directory for Part 6.
3. You're done with some code changes now; make a commit!
   * Make sure to `git add` the `main.cpp` file.
   * Use `git status` to make sure you didn't miss anything.
   * Use `git commit` to save a version of your code including your changes.
     Write a short message describing your changes.
   * Use `git push` to sync your code history to the GitHub server.

## Part 5: Analyze

**NOTE: This part *cannot* be done on the lab computers, as it requires
administrative access.** If you do not have a CUDA-capable computer of your
own, you may need to borrow one for this part. However, you can still do the
rest of your development on the lab computer.

### Windows

1. Go to the Nsight menu in Visual Studio.
2. Select *Start Performance Analysis...*.
3. Select *Trace Application*. Under *Trace Settings*, enable tracing for CUDA and OpenGL.
4. Under *Application Control*, click *Launch*.
   * If you have switchable graphics (NVIDIA Optimus), see the note in Part 3.
5. Run the program for a few seconds, then close it.
6. At the top of the report page, select *Timeline* from the drop-down menu.
7. Take a screenshot of this tab and save it to `images`, for Part 6.

### OS X & Linux

1. Open your project in Nsight.
2. *Run*->*Profile*.
3. Run the program for a few seconds, then close it.
4. Take a screenshot of the timeline and save it to `images`, for Part 6.


## Part 6: Write-up

1. Update ALL of the TODOs at the top of this README:
   * Finish your `README.md`
   * Add your name, computer, and whether it's a personal or lab computer.
   * Embed the screenshots you took: `![](images/example.png)`
   * Syntax help: https://help.github.com/articles/writing-on-github/
2. Add, commit, and push your screenshots and README.
   * Make sure your README looks good on GitHub!
3. If you have modified either of the `CMakeLists.txt` at all (aside from
   the list of `SOURCE_FILES`), mention it explicitly.

## Submit
Open a GitHub pull request so that we can see that you have finished.
The title should be "Proj 0 Submission: YOUR NAME".
The template of the comment section of your pull request is attached below, you do some copy and modify:  

* [Repo Link](https://link-to-your-repo)
* `Your PENNKEY`
* (Briefly) Mentions features that you've completed. Especially those bells and whistles you want to highlight
    * Feature 0
    * Feature 1
    * ...
* Feedback on the project itself, if any.

And you're done!
