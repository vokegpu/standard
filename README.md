# Code of Conduct and Coding Style Guide for Vokegpu Projects

All written here is strictly followed, may some older projects contains unaltered coding style but EKG must refactor soon.

# Summary

User-programmer: an user that is a programmer and is using a technology from Vokegpu.  
Internal: no user-programmer side purpose, only for the library engine.  
Features: object(s), data(s) or any technology from Vokegpu.

# Library Coding Guide-Style

* Use 2 (two) spaces as tab.
* Standard case is sneak_case, SCREAM_SNEAK_CASE for macro(s).
* No unnecessary macro(s), use `constexpr`, for type-definitions use `typedef`.
* Ptr(s) must starts with `p_*`.
* Use `this->` and not `m_*`.
* Definitions on header(s) are trivial but do not use too much.
* C-style references are allowed `int *p_bla` but if possible use `int &bla`.
* Struct(s) are not allowed to have method(s), if contains, must be declared as `class` and not `struct`.
* Non-OO (Object Oriented) or struct without method(s) must end as type `*_t`.

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

* - Public user-programmer side object(s) and data(s), must not be by-package namespace separated.
```c++
// gpu/model.hpp
namespace lib {
  struct model_t {
  public:
    // bla
  };
}

namespace lib {
   lib::flags_t create_model(lib::model_t &model);

   // or C++ way
   lib::flags_t create_model(lib::model_t *p_model);
};
```
