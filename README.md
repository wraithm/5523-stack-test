# The problem

Stack puts indentation in front of GHC output. This blocks emacs and vim from parsing the output and
tracking those errors.

## Comparison

### Old version of stack

``` shell
$ stack --version
Version 2.5.1, Git revision d6ab861544918185236cf826cb2028abb266d6d5 x86_64 hpack-0.33.0
$ stack build --no-interleaved-output
Building all executables for `bad' once. After a successful build of all of them, only specified executables will be rebuilt.
bad> configure (exe)
bad> build (exe)
Log files have been written to: /path/to/5523-stack-test/.stack-work/logs/

--  While building package bad-0.1.0 (scroll up to its section to see the error) using:
      /home/user/.stack/setup-exe-cache/x86_64-linux-tinfo6/Cabal-simple_mPHDZzAJ_3.2.1.0_ghc-8.10.4 --builddir=.stack-work/dist/x86_64-linux-tinfo6/Cabal-3.2.1.0 build exe:bad --ghc-options ""
    Process exited with code: ExitFailure 1
    Logs have been written to: /path/to/5523-stack-test/.stack-work/logs/bad-0.1.0.log

    Configuring bad-0.1.0...
    Preprocessing executable 'bad' for bad-0.1.0..
    Building executable 'bad' for bad-0.1.0..
    [1 of 2] Compiling Main

    /path/to/5523-stack-test/bad/Main.hs:4:47: error:
        lexical error in string/character literal at character '\n'
      |
    4 | main = putStrLn "This is a blatant parse error
      |                                               ^

```

### New version of stack

``` shell
$ ../stack/stack --version
Version 2.6.0, Git revision 21223c306df528f75e769d1eef5ed4bf8d916129 (8305 commits) PRE-RELEASE x86_64 hpack-0.33.0
$ ../stack/stack build --no-interleaved-output
Building all executables for `bad' once. After a successful build of all of them, only specified executables will be rebuilt.
bad> configure (exe)
bad> build (exe)
Log files have been written to: /path/to/5523-stack-test/.stack-work/logs/

--  While building package bad-0.1.0 (scroll up to its section to see the error) using:
      /home/user/.stack/setup-exe-cache/x86_64-linux-tinfo6/Cabal-simple_mPHDZzAJ_3.2.1.0_ghc-8.10.4 --builddir=.stack-work/dist/x86_64-linux-tinfo6/Cabal-3.2.1.0 build exe:bad --ghc-options " -fdiagnostics-color=always"
    Process exited with code: ExitFailure 1
    Logs have been written to: /path/to/5523-stack-test/.stack-work/logs/bad-0.1.0.log

Configuring bad-0.1.0...
Preprocessing executable 'bad' for bad-0.1.0..
Building executable 'bad' for bad-0.1.0..
[1 of 2] Compiling Main

/path/to/5523-stack-test/bad/Main.hs:4:47: error:
    lexical error in string/character literal at character '\n'
  |
4 | main = putStrLn "This is a blatant parse error
  |                                               ^

```
