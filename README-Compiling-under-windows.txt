

PYDISTMESH - Installation on Windows
mz, 2014/06/28

In order to install PYDISTMESH on Windows you need:

A python distribution with NUMPY installed. I use WinPython. Please note:
-  you have to copy the numpy headers from ./Lib/site-packages/numpy/core/include 
   to ./include

As compiler use:
1) Microsoft Visual Studio Express 2010
2) Microsoft 7.1 SDK (for 64-bit OS)

In addition the following DLLs are needed:
- liblapack.dll, libblas.dll, lapack.lib, blas.lib (32-bit / 64-bit, MinGW version)
- From MinGW: libgfortran-3.dll, libgcc_s_dw2-1.dll, libgcc_s_seh_64-1.dll, 
  libgcc_s_sjlj-1.dll, libquadmath_64-0.dll 
  (All either 32-bit or 64-bit. The exact naming depends on the MinGW distribution)
The DLL files have to be copied to ./libs and to ./Lib/site-packages/distmesh after 
the python package installation

Change DISTMESH as follows:
- Rename *.c files to *.cpp (2 files)
- Update include statement in _distance_functions.cpp
- Update _distance_functions.pyx, setup.py to .cpp
- Add the following to src/distance_functions.cpp below #include <math.h
	#ifdef _MSC_VER
	#define INFINITY (DBL_MAX+DBL_MAX)
	#define NAN (INFINITY-INFINITY)
	#endif

To build DISTMESH:
1) Open the Visual Studio Command Prompt (32-bit) or the Windows 7 SDK Command Prompt
2) Execute set VS90COMNTOOLS=%VS100COMNTOOLS%
3) Go to the DISTMESH source directory
4) and execute:
     /path/to/winpython/python.exe setup.py build
	 /path/to/winpython/python.exe setup.py install
5) copy all DLL from aove to ./Lib/site-packages/distmesh

Verify that all dependencies are met for ./Lib/site-packages/distmesh/_distance_functions.pyd
via DependecyWalker

Test DISTMESH via:
/path/to/winpython/python.exe -m distmesh.demo2d



  

  


  

  
  
