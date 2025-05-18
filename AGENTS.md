# general instructions
- Only modify Rust files (*.rs). Don't modify any other file types.
- Never modify C source or header files (*.c, *.h).
- Never modify assembly files (*.S, *.asm) or build files (*.meson).
- The C program is a high-performance AV1 decoder called dav1d.
- The Rust code was generated automatically by a tool called c2rust using C
  source files as input. For instance, the file `src/cdef.rs` was generated
  from the C source file `src/cdef.c`. C source files ending in _tmpl.c are
  special template files that are compiled twice with different preprocessor
  definitions. The files `src/cdef_tmpl_8.rs` and `src/cdef_tmpl_16.rs` were both
  generated from the C file `src/cdef_tmpl.c` (for bitdepths 8 and 16
  respectively).
- Maintaining high performance is very important. Changes to the Rust code should
  maintain the same structure as the C code and use the same algorithms to the
  extent it can be expressed as idiomatic and readable Rust.
- All Rust changes must successfully build and pass all tests. Instructions below.

# build instructions
- `cargo build --release`

# test instructions
- `.github/workflows/test.sh`

- A successful test run will show 790 passing tests and 0 failures. Example output:
```
780/790 dav1d:testdata-12 / 00000787                                                    OK              0.01s
781/790 dav1d:testdata-12 / 00000788                                                    OK              0.01s
782/790 dav1d:testdata-12 / 00000789                                                    OK              0.01s
783/790 dav1d:testdata-12 / 00000790                                                    OK              0.01s
784/790 dav1d:testdata-12 / 00000791                                                    OK              0.01s
785/790 dav1d:testdata-12 / lossless                                                    OK              0.00s
786/790 dav1d:testdata-8 / autostitch-480p-240p-160p-10s                                OK              0.32s
787/790 dav1d:testdata-multi / test10100_579_8614                                       OK              0.07s
788/790 dav1d:testdata-10 / issue_318                                                   OK              0.34s
789/790 dav1d:testdata-12 / test16153                                                   OK              0.25s
790/790 dav1d:testdata-8 / autostitch-480p-240p-160p                                    OK              0.67s


Ok:                 790
Expected Fail:      0
Fail:               0
Unexpected Pass:    0
Skipped:            0
Timeout:            0

Full log written to /home/joeuser/rav1d/build/meson-logs/testlog.txt
```

