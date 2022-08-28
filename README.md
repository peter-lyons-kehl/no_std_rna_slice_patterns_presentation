Features of each pattern

| Feature | [01](https://github.com/peter-kehl/no_std_rna_transcription_patterns/blob/main/01_ok_heap-string/src/lib.rs "01_ok_heap-string") |
[02](https://github.com/peter-kehl/no_std_rna_transcription_patterns/blob/main/)
[03](https://github.com/peter-kehl/no_std_rna_transcription_patterns/blob/main/)
[03](https://github.com/peter-kehl/no_std_rna_transcription_patterns/blob/main/)
[03](https://github.com/peter-kehl/no_std_rna_transcription_patterns/blob/main/)
[03](https://github.com/peter-kehl/no_std_rna_transcription_patterns/blob/main/)
[03](https://github.com/peter-kehl/no_std_rna_transcription_patterns/blob/main/)
[03](https://github.com/peter-kehl/no_std_rna_transcription_patterns/blob/main/)
[03](https://github.com/peter-kehl/no_std_rna_transcription_patterns/blob/main/)
[03](https://github.com/peter-kehl/no_std_rna_transcription_patterns/blob/main/)
[03](https://github.com/peter-kehl/no_std_rna_transcription_patterns/blob/main/)
[03](https://github.com/peter-kehl/no_std_rna_transcription_patterns/blob/main/)
[03](https://github.com/peter-kehl/no_std_rna_transcription_patterns/blob/main/)
[03](https://github.com/peter-kehl/no_std_rna_transcription_patterns/blob/main/)
[03](https://github.com/peter-kehl/no_std_rna_transcription_patterns/blob/main/)
[03](https://github.com/peter-kehl/no_std_rna_transcription_patterns/blob/main/)
[03](https://github.com/peter-kehl/no_std_rna_transcription_patterns/blob/main/)
[03](https://github.com/peter-kehl/no_std_rna_transcription_patterns/blob/main/)
[03](https://github.com/peter-kehl/no_std_rna_transcription_patterns/blob/main/)

| --- | --- |
|extra work for securing observability/serialization: array or passed-in mutable slice could leak data!|
|same compile-time limit for all instances (one type) <-> various compile-time limits per instance (generic type), can have a default limit <-> no compile-time limit|
|random access (data storage) <-> sequential access only|
| string data-specific: Unicode needs extra handling (04.. - anything with _bytes) <-> Unicode out of the box|
| -- (Not `no_std` specific, but it matters in these examples.)|
| field storage: owned <-> passed-in|
| into_rna(): consume the original <-> refer to (the original) with a lifetime <-> copy (the original), no lifetime|
| mutable (including "resize" of the valid/active data) - limited mutation (can't "resize") - immutable|
| owned value (no lifetime) - lifetimed|
| Clone - no Clone|
|Clone derivable - not derivable or no Clone|
|Copy - non-Copy (or `Copy` would be insecure).|
|different types for mutation and for sharing: 06_slice-pass_in|
| --- |
|`dyn` (virtual) dispatch <-> static (compile-time) dispatch|
| extra dispatch methods |
| --- |
| thread safe (`Sync` - if used in `std`) -> TODO "tests": `struct EnsureSync<T: Sync>; type _EnsureSyncRna = EnsureSync<Rna>;` We could use a (compile time) crate feature and conditional compilation to switch between single-threaded `Cell` and alternative ways, including https://docs.rs/mitochondria (`no_std`-friendly), https://docs.rs/lazycell, https://docs.rs/lazy-init. But then we couldn't easily test them all in the same workspace.