# Code of Conduct and Coding Style Guide for Vokegpu Projects

## Preface

All written here is strictly followed, may some older projects contains unaltered coding style but EKG must refactor soon.  
For libraries, you must follow the user-programmer side concept, if the project is an application, follow as the core of library.

---

## Summary, Commit-Format, and Library Coding Guide-Style

### Summary

User-programmer: an user that is a programmer and is using a technology from Vokegpu.  
Internal: no user-programmer side purpose, only for the library engine.  
Features: object(s), data(s) or any technology from Vokegpu.

### Commit-Format

Commit formatting is important, sadly VokeGpu is not total mature, but we should follow it now.

Basic:  
`[commit-type] thing 1; thing 2; thing ...`

If possible add a description for specific-topics:  
`bla, bla, meow`

Also, concant commits-types if possible:  
`[feature][update][fix] added colored-buttons; updated slider code; fixed a glitch where meow spells on the console`

Commit-types:  
* `[update]` updated any-feature
* `[feature]` added a feature
* `[fix]` fixed something like a glitch or performance-issues
* `[ref]` refactored code, like code-format, nomenclature or any moved stuff
* `[git]` any related git stuff
* `[deprecated]` specific-case where you deprecated anything
* `[build]` build-file was changed

### Library Coding Guide-Style

* Use `#ifndef LIB_PACKAGE_FEATURE_HPP` for headers, for platform-specific code use `#if defined(X)`
```c++
#ifndef LIB_PACKAGE_FEATURE_HPP
#define LIB_PACKAGE_FEATURE_HPP

namespace lib {
  void meow() {
    #if defined(X)
      // do something here
    #else
      // moo
    #endif

    #if defined(Y)
      meow();
    #endif
  }
}

#endif
```

* Use 2 (two) spaces as tab.
* Standard case is sneak_case, SCREAM_SNEAK_CASE for macro(s).
* No unnecessary macro(s), use `constexpr` if possible, for type-definitions use `typedef`.
* Ptr(s) must starts with `p_*`, and counts many `***`, e.g: `int ***ppp_bla`.
* Use `this->` and not `m_*`.
* Definitions on header(s) are trivial but do not use too much.
* C-style references are allowed `int *p_bla` but if possible use `int &bla`.
* Struct(s) are not allowed to have method(s), if contains, must be declared as `class` and not `struct`.
* Non-OO (Object Oriented) or struct without method(s) must end as type `*_t`.

* - Internal-object(s) and internal-data(s) must be by-package namespace separated.
```c++
// all `lib::gpu` are used by the core of library

// gpu/model.hpp
namespace lib::gpu {
  struct instance_t {
  public:
    // etc
  };

  lib::flags_t create_instance(
    lib::gpu::create_instance_info_t *p_create_instance_info,
    lib::gpu::instance_t *p_instance
  );
}
```

* - Public user-programmer side object(s) and data(s), must not be by-package namespace separated.
```c++
// all `lib` are used by the core of library at same time is public for the user-programmer side.

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
