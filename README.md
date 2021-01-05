# zsh gtest completion

Zsh tabcompletion definition for executables built with [gtest](https://github.com/google/googletest/).

## Installation

Put the `_gtest` file into a directory in your `$fpath`.

I leave it up to you / your operating system / plugin management system / zshrc
configuration to figure out how to best do this. This may be adding the
repository's path to `$fpath` or `$FPATH`, copy or symlink the completion file
into an existing direcotry in the `fpath`. In any case the last change to the
value of `fpath` should happen before `compinit` gets called. I suggest to
persistify this and nor repeat once per project / test binary / testing
session.

## Usage

Suppose the build system has produced a binary called `my_test_executable` in the directory `builddir/tests/`.

Setup
```
compdef _gtest my_test_executable
```

Completion
```
./builddir/tests/my_test_executable --⇥
option:
--gtest_also_run_disabled_tests  -- Run all disabled tests too.
--gtest_break_on_failure         -- Turn assertion failures into debugger break-points.
--gtest_catch_exceptions         -- Do not report exceptions as test failures. Instead, allow them to crash the program or throw a pop-up (on Windows).
--gtest_color                    -- Enable/disable colored output.
--gtest_death_test_style         -- Set the default death test style.
--gtest_filter                   -- Filter tests to run by positive and negative patterns.
--gtest_list_tests               -- List the names of all tests instead of running them.
--gtest_output                   -- Generate a JSON or XML report
--gtest_print_time               -- Print elapsed test time
--gtest_random_seed              -- Random number seed to use for shuffling test orders
--gtest_repeat                   -- Run the tests repeatedly; use a negative count to repeat forever.
--gtest_shuffle                  -- Randomize tests' orders on every iteration.
--gtest_stream_result_to         -- Stream test results to the given server.
--gtest_throw_on_failure         -- Turn assertion failures into C++ exceptions for use by an external test framework.
--help                           -- Print usage message and exit.
```

In my experience it suffices to manually call `compdef` once per test binary
and once per debugging session.  A per-project setup that doesn't need to be
repeated per session/shell launch wasn't necessary for me. If you have
per-project `setup.zsh` files, a persistent compdef setup might be better
suited for you.

## Notes

I'm using settings such as

```
zstyle ':completion:*:descriptions' format $'%{\e[0;33m%}%d:%{\e[0m%}'
zstyle ':completion:*:messages' format $'%{\e[0;31m%}%d%{\e[0m%}'
```

Absence of `messages` or `description` printing may lead to a different
printout of the completion than what I intended.

## License

This completion is under the [BSD 3-Clause License](LICENSE), just like the gtest framework.
