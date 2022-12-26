# CMake Project Commands

Add CMake commands for project-centric builds.

Modern CMake relies on `target_*` commands for constructing targets with the
correct property visibilities. One common structure is to define a `project()`
for each target and always use `${PROJECT_NAME}` as the target name for the
target commands. In this approach, `${PROJECT_NAME}` gets repeated over and over
again.

CMake functions can easily deal with this repetition.  Simply include
`cmake_project_commands.cmake` to your build and use the provided commands. For
each `target_` command in base CMake, there is an equivalent `project_` version
that just assumes the target is the current value of `${PROJECT_NAME}`.

For example, the following CMake:

```cmake
project(myProject)
add_executable(${PROJECT_NAME} main.cpp)
target_link_libraires(${PROJECT_NAME} PRIVATE otherProject)
```

...would instead become:

```cmake
project(myProject)
project_add_executable(main.cpp)
project_link_libraires(PRIVATE otherProject)
```
