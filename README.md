# Code of Conduct and Coding Style Guide for Vokegpu Projects

All written here is strictly followed, may some older projects contains unaltered coding style but EKG must refactor soon.

# Summary

User-programmer: an user that is a programmer and is using a technology from Vokegpu.  
Internal: no user-programmer side purpose, only for the library engine.  
Features: object(s), data(s) or any technology from Vokegpu.

# Library Coding Guide-Style

* Standard case is sneak_case, SCREAM_SNEAK_CASE for macro(s).
* No macro(s), use `constexpr` or `typedef`.
* Ptr(s) must be starts with `p_*`.
* Use `this->` and not `m_*`.
* Definitions on header(s) are trivial but do not use too much.

* - Internal-object(s) and internal-data(s) must be by-package namespace separated.
```c++
// gpu/model.hpp
namespace lib::gpu {
  struct instance_t {
  public:
    // etc
  };

  lib::flags_t create_instance(
    lib::create_instance_info_t *p_create_instance_info,
    lib::gpu::instance_t *p_instance
  );
}
```

* 2- Public user-programmer side object(s) and data(s), must not be by-package namespace separated.
```c++
// gpu/model.hpp
namespace lib::gpu {
  
}
```
 
* 3- Non-OO (Object Oriented) or struct without method(s) must end as type `*_t`.
* 4- Struct(s) are not allowed to have method(s), if contains, must be declared as `class` and not `struct`.
* 5- 

```
* All user-programmer side features, must be no longer by-package namespace separated.  

* 2- Only internal-objects and internal-features must be by-package namespace separated.
```c++
// ekg/ui/frame
namespace ekg {
  struct frame_t {
  public:
    // descriptor fields
  }
}

namespace ekg::ui {
  struct frame : public ekg::ui::abstract {
  public:
    // frame widget fields
  }
}
```

* 3- Non-OO features as descriptors, must end as a type `*_t`, and not a class.

* 4- OO features must be a class.

* 5- `typedef` must end as a type `*_t`.

* 6- `extern` fields must be public `ekg::` namespace and not private `ekg::*private*::` namespace(s).

* 7- Any service or specialized-manager must contains `init` and `quit` methods, same it is useless at moment.
```
