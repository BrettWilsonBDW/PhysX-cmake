## PhysX with a simple CMake to be used with FetchContent

### example use


```bash
include(FetchContent)
FetchContent_Declare(physx}
  GIT_REPOSITORY https://github.com/BrettWilsonBDW/PhysX-cmake.git
  GIT_TAG head
  GIT_SHALLOW    TRUE
  GIT_PROGRESS   TRUE
)
FetchContent_MakeAvailable(${dep})
```

####
Acknowledgements

- https://github.com/NVIDIA-Omniverse/PhysX
