# Code of Conduct and Coding Style Guide for Vokegpu Projects

## Preface

### Note

All written here is strictly followed, may some older projects contains unaltered coding style but EKG must refactor soon.

### Summary

`User-programmer` - an user that is a programmer and is using a technology from Vokegpu.  
`Internal` - no user-programmer side purpose, only for the library engine.  
`Features` - object(s), data(s) or any technology from Vokegpu.

---

## Commit and Version

### Commit

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

### Version

Any software from VokeGpu MUST has a paper named `commit.txt` under `version` dir, where you can describe what was created, updated or deleted.
```
[version e.g: 1.0.0] [date e.g: 04/06/2025]

-- [description: removed moo]
-- [description: something glitch idk]

[version e.g: 1.1.0] [date e.g: 10/07/2025]

-- [description e.g: bla added meow]

etc

```

Most recent version must be always at end.  
With auto-release, we can describe a complete history-change and details.

---

## The Programming Standard for Building VokeGpu Technologies 

### Architecture 

Building a project with support for 32 bits must use at maxium 4-bytes number, as example, declaring `flags_t` or `id`:
```cpp
namespace * {
  typedef uint32_t flags_t;
  typedef uint32_t id_t;
};
```

If the project purpose is not support 32-bits, reaching 8-bytes is not a rule, this applies for all parts of code, every field, function, method etc.

### Library-Standard

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
* Standard case is `sneak_case`, `SCREAM_SNEAK_CASE` for macro(s), optionally (`SCREAM_SNEAK_CASE`, `sneak_case`, `nocase`, `SCREAMNOCASE`) for enum(s) --- but no mistakes, do not use `SCREAMNOCASE` enum(s) with `nocase`, we do not care if you use `nocase` and `sneak_case` for enum(s), just if you mix `SCREAM_SNEAK_CASE` with `sneak_case`.
* No unnecessary macro(s), use `constexpr` if possible, for type-definitions use `typedef`.
* Ptr(s) must starts with `p_*`, and counts many `***`, e.g: `int ***ppp_bla`.
* Use `this->` and not `m_*`.
* Definitions on header(s) are trivial but do not use too much.
* C-style references are allowed `int *p_bla` but if possible use `int &bla`.
* Struct(s) are not allowed to have method(s), if contains, must be declared as `class` and not `struct`.
* Non-OO (Object Oriented) or struct without method(s) must end as type `*_t`.
* Library output dir must be located in: `lib/OS/32|64`.

* - Internal-object(s) and internal-data(s) must be by-package namespace separated, you can optionally complete the package namespace sentence, but do not mix, follow a pattern.
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

### Software-Standard

All must follow as core-library, except:

* Executable output dir must be located in: `bin/OS/32|64`.

* Internal-feature(s) if are used on genernal-specific places must be by-package namespace separated, otherwise, you do not need to put everything on separated namespace.
```cpp
// genernal-specific internal-feature(s)
namespace application::* {
  /**
   * This is genernally used on specific parts of the code, not all places.
   **/
  application::flags_t fetch(/* etc */);
}

// general features(s)
namesplace application {
  typedef uint64_t flags_t;

  enum make {
    MEOW,
    MOO
  }; 

  template<typename t>
  t meow() {
    return t {};
  }

  /**
   * This can be used in EVERYTHING!
   **/
  class log {
  public:
     /* etc */ 
  };
}
```
