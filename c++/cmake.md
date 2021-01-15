---
title: CMake
parent: C++
---

Jetbrains Developer Survey
	Cmake: 36%. Makefiles 24%
Watched video: C++ Weekly - Ep 78 - Intro to CMake
	* Cmake more in-depth study
		target_compile_features
		http://aosabook.org/en/cmake.html
		Cmake book: https://www.kitware.com/what-we-offer/#books
		Project: https://github.com/Kitware/CMake
	* C++14 lambda functions
	* Enabling compiler warnings
		Including: -Wall -Wextra -Wpedantic
Read Wikipedia
	Experts now advise to avoid variables in favor of targets and properties. The commands add_compile_options, include_directories, link_directories, link_libraries that were at the core of CMake 2 should now be replaced by target-specific commands.
		https://github.com/boostcon/cppnow_presentations_2017/blob/master/05-19-2017_friday/effective_cmake__daniel_pfeifer__cppnow_05-19-2017.pdf
	* CPack can generate Linux packages RPM, deb, etc.
Cmake website: https://cmake.org/
	A main benefit is for cross-platform development.
