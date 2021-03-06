# Changelog

All notable changes to the `pythonwhat` project will be documented in this file. This project adheres to [Semantic Versioning](http://semver.org/spec/v2.0.0.html).

## 2.12.3

### Added

- Whether or not something should be highlighted can be specified through the state now
- You can use `<other_fun>.disable_highlighting().<anohter_fun>` anywhere in the SCT chain to disable highlighting.

### Changed

- There are no more `highlight` arguments in any `pythonwhat` SCT functions.
- `Feedback` now takes a state from which it reads which part should be highlighting and whether it should be highlighted.
- Use of `StubState` to trick the system somewhat, should be refactored at some point, but works fine.
- `test_function_v2()` and `test_function()` only higlight if the `index = 1`, i.e. when the first call of a certain function is being checked. Added tests (and updated other tests) accordingly.

## 2.12.2

### Added

- In `check_args()`, you can now use `['args', 0]` and `['kwargs', 'a']` to look for matched positional star args, and matched named star args.
  The docs have been updated accordingly: https://pythonwhat.readthedocs.io/en/stable/articles/checking_function_calls.html

### Changed

- The equality checks for lists, dicts, numpy arrays, pandas dataframes and pandas series have been made faster, without compromising backwards compatibility.

### Fixed

- There was a nasty bug with signature binding when using `check_function()` for the same function when this function took only positional args. This would alleviate the need of any `signature=False` usage, once and for all!

## 2.12.1

### Added

- Reference documentation now contains examples for `set_context()` and `set_env()`.
- A `tests/test_debug.py` file has been added to easily test questions that CDs might have.

### Changed

- There was a bug in the feedback message generation for errors. It now just refers to the console.


## 2.12.0

### Added

- All new `has_()` functions are now properly documented, so there should be no reason for you to use a `test_` function other than `test_or` and `test_correct`. If you do find yourself using it (because you don't know the alternative), ping me and we'll talk!
- Added documentation on the `check_function_def()` related functions.
- `index = 0` is now a default for functions like `check_if_else()`, `check_function()` etc.
- Like there is `set_context`, there is now `set_env` to set environment variables before using something like `has_equal_value()`. These `set_` functions serve as alternatives for the `extra_env` and `context_vals` arguments that appear in many functions and that I plan to discontinue at some point.
- Added a `test_` to `check_` article, that explains how you can go from old-style to new-style SCTs. Feel free to contribute!!

### Changed

- If you experiment locally, you will now see the feedback message that the SCT chain would generate (this is explained in the README on GitHub):

```Python
from pythonwhat.local import setup_state
s = setup_state(sol_code = "x = 4", stu_code = "x = 5")
s.check_object('x').has_equal_value()
# <traceback omitted>
# pythonwhat.Test.TestFail: Check the variable `x`. Unexpected expression value: expected `4`, got `5`.
```

- The glossary is featured more prominently in the docs, as it is a good resource to see how everything fits together.

### Removed

- There is no support for `keep_objs_in_env`, as nobody is using it.