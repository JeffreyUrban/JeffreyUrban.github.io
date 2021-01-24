---
title: CMake
parent: C++
---

[Main Site](https://cmake.org/)

[Repo](https://github.com/Kitware/CMake)

[History, Approach and Lessons](http://aosabook.org/en/cmake.html)

[Best Practices](https://github.com/boostcon/cppnow_presentations_2017/blob/master/05-19-2017_friday/effective_cmake__daniel_pfeifer__cppnow_05-19-2017.pdf)

Reasons to choose CMake:
- Useful for cross-platform development.
- Jetbrains Developer Survey shows CMake more popular at 36% preference vs Makefiles at 24%.

Notables:

- Popular compiler warnings `-Wall -Wextra -Wpedantic`

- These core commands from CMake 2 have been obsoleted, and should now be replaced by target-specific commands:

    `add_compile_options`, `include_directories`, `link_directories`, `link_libraries`

- Best to avoid variables in favor of targets and properties.


Add expected compiler features to a target: `target_compile_features`

Generate Linux packages _(RPM, deb, etc.)_: see CPack

