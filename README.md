# Prerequisites

- `nightly` Rust compiler
 - the actual solutions work with `stable` Rust. However, the test harness (with extras on top of of
   Exercism's tests) needs `nightly` (as of mid 2022).

# List of patterns (and shared utils)
These [examples](https://github.com/peter-kehl/no_std_rna_slice_patterns) are ordered as they progress:
- [00_utils](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/00_utils/src/lib.rs)
- [01_ok_heap-string](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/01_ok_heap-string/src/lib.rs)
- [02_no_heap-array-const_limit-chars](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/02_no_heap-array-const_limit-chars/src/lib.rs)
- [03_no_heap-array-const_limit-bytes-wipe_on_mut](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/03_no_heap-array-const_limit-bytes-wipe_on_mut/src/lib.rs)
- [04_no_heap-array-const_limit-bytes-wipe_on_clone](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/04_no_heap-array-const_limit-bytes-wipe_on_clone/src/lib.rs)
- [05_no_heap-array-const_limit-bytes-wipe_on_clone-unsafe](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/05_no_heap-array-const_limit-bytes-wipe_on_clone-unsafe/src/lib.rs)
- [06_no_heap-array-const_generic_exact-bytes](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/06_no_heap-array-const_generic_exact-bytes/src/lib.rs)
- [07_no_heap-array-const_generic_limit-bytes-wipe_on_mut](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/07_no_heap-array-const_generic_limit-bytes-wipe_on_mut/src/lib.rs)
- [08_no_heap-array-const_generic_limit-bytes-wipe_on_clone](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/08_no_heap-array-const_generic_limit-bytes-wipe_on_clone/src/lib.rs)
- [09_no_heap-slice-pass_in-bytes-wipe_on_mut](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/09_no_heap-slice-pass_in-bytes-wipe_on_mut/src/lib.rs)
- [10_no_heap-slice-pass_in-bytes-wipe_on_drop](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/10_no_heap-slice-pass_in-bytes-wipe_on_drop/src/lib.rs)
- [11_ok_heap-slices-box_dyn_trait-map](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/11_ok_heap-slices-box_dyn_trait-map/src/lib.rs)
- [12_no_heap-slices-iterator_enum](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/12_no_heap-slices-iterator_enum/src/lib.rs)
- [13_no_heap-slices-iterator_impl](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/13_no_heap-slices-iterator_impl/src/lib.rs)
- [14_no_heap-eq_branch_iterators-dyn_trait](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/14_no_heap-eq_branch_iterators-dyn_trait/src/lib.rs)
- [15_no_heap-eq_branch_iterators-matrix](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/15_no_heap-eq_branch_iterators-matrix/src/lib.rs)
- [16_no_heap-eq_iterator_to_generic_fn](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/16_no_heap-eq_iterator_to_generic_fn/src/lib.rs)
- [17_no_heap-eq_dispatch_specialized](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/17_no_heap-eq_dispatch_specialized/src/lib.rs)
- [18_no_heap-eq_dispatch_universal](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/18_no_heap-eq_dispatch_universal/src/lib.rs)
---

# Features of patterns
| Feature | [01](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/01_ok_heap-string/src/lib.rs "01_ok_heap-string") | [02](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/02_no_heap-array-const_limit-chars/src/lib.rs "02_no_heap-array-const_limit-chars") | [03](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/03_no_heap-array-const_limit-bytes-wipe_on_mut/src/lib.rs "03_no_heap-array-const_limit-bytes-wipe_on_mut") | [04](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/04_no_heap-array-const_limit-bytes-wipe_on_clone/src/lib.rs "04_no_heap-array-const_limit-bytes-wipe_on_clone") | [05](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/05_no_heap-array-const_limit-bytes-wipe_on_clone-unsafe/src/lib.rs "05_no_heap-array-const_limit-bytes-wipe_on_clone-unsafe") | [06](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/06_no_heap-array-const_generic_exact-bytes/src/lib.rs "06_no_heap-array-const_generic_exact-bytes") | [07](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/07_no_heap-array-const_generic_limit-bytes-wipe_on_mut/src/lib.rs "07_no_heap-array-const_generic_limit-bytes-wipe_on_mut") | [08](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/08_no_heap-array-const_generic_limit-bytes-wipe_on_clone/src/lib.rs "08_no_heap-array-const_generic_limit-bytes-wipe_on_clone") | [09](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/09_no_heap-slice-pass_in-bytes-wipe_on_mut/src/lib.rs "09_no_heap-slice-pass_in-bytes-wipe_on_mut") | [10](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/10_no_heap-slice-pass_in-bytes-wipe_on_drop/src/lib.rs "10_no_heap-slice-pass_in-bytes-wipe_on_drop") | [11](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/11_ok_heap-slices-box_dyn_trait-map/src/lib.rs "11_ok_heap-slices-box_dyn_trait-map") | [12](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/12_no_heap-slices-iterator_enum/src/lib.rs "12_no_heap-slices-iterator_enum") | [13](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/13_no_heap-slices-iterator_impl/src/lib.rs "13_no_heap-slices-iterator_impl") | [14](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/14_no_heap-eq_branch_iterators-dyn_trait/src/lib.rs "14_no_heap-eq_branch_iterators-dyn_trait") | [15](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/15_no_heap-eq_branch_iterators-matrix/src/lib.rs "15_no_heap-eq_branch_iterators-matrix") | [16](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/16_no_heap-eq_iterator_to_generic_fn/src/lib.rs "16_no_heap-eq_iterator_to_generic_fn") | [17](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/17_no_heap-eq_dispatch_specialized/src/lib.rs "17_no_heap-eq_dispatch_specialized") | [18](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/18_no_heap-eq_dispatch_universal/src/lib.rs "18_no_heap-eq_dispatch_universal") |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Implemented | * | * | * | * | * | * | | | part | | * | * | * | * | * | * | * | * |
| extra work for securing observability/serialization: array or passed-in mutable slice could leak data! |
| fixed compile-time size limit for all instances (one type) | | * | * | * | * | | | | | | | | | | | | | |
| various compile-time size limits per instance (generic type), can have a default limit | | | | | | * | * | * | | | | | | | | | | |
| no compile-time limit | * |  |  |  |  |  |  |  | * | * | * | * | * | * | * | * | * | * |
| random access & data storage (rather than sequential access only) | * | * | * | * | * | * | * | * | * | * |  |  |  |  |  |  |  |  |
| string data-specific: Unicode needs extra handling (04.. - anything with _bytes) <-> Unicode out of the box |
| -- (Not `no_std` specific, but it matters in these examples.) |
| field storage: owned <-> passed-in |
| into_rna(): consume the original <-> refer to (the original) with a lifetime <-> copy (the original), no lifetime |
| mutable (including "resize" of the valid/active data) - limited mutation (can't "resize") - immutable |
| owned value (no lifetime) - lifetimed |
| Clone - no Clone |
| Clone derivable - not derivable or no Clone |
| Copy - non-Copy (or `Copy` would be insecure). |
| different types for mutation and for sharing: 06_slice-pass_in |
| --- |
|`dyn` (virtual) dispatch <-> static (compile-time) dispatch |
| extra dispatch methods |
| --- |
| thread safe (`Sync` - if used in `std`) -> TODO "tests": `struct EnsureSync<T: Sync>; type _EnsureSyncRna = EnsureSync<Rna>;` We could use a (compile time) crate feature and conditional compilation to switch between single-threaded `Cell` and alternative ways, including https://docs.rs/mitochondria (`no_std`-friendly), https://docs.rs/lazycell, https://docs.rs/lazy-init. But then we couldn't easily test them all in the same workspace. |
