TODO
- beware that vscode.dev can't display inferred types (of `let` definitions), neither declared
  parameter names in function calls
- vote for [enabling rust-analyzer on vscode.dev](https://github.com/rust-lang/rust-analyzer/issues/11309)
- https://github.dev/peter-kehl/no_std_rna_slice_patterns
  - VS-Code-like horizontal menu (if you have it hidden by default, toggle it with "Alt")
  - your VS Code theme (if you use VS Code sync)
  - `Ctrl + comma` shows VS-Code-like Settings
- Alternative online VS Code:
 - https://vscode.dev/github/peter-kehl/no_std_rna_slice_patterns
 - [Insiders (beta-like version)](https://insiders.vscode.dev/github/peter-kehl/no_std_rna_slice_patterns)
 - these don't have a horizontal menu, but open it by the hamburger button

---
# Prerequisites

- `nightly` Rust compiler
 - the actual solutions work with `stable` Rust. However, the test harness (with extras on top of of
   Exercism's tests) needs `nightly` (as of mid 2022).

# List of patterns (and shared utils)
- [00_utils](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/00_utils/src/lib.rs)
- [00_test_harness](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/00_test_harness/src/lib.rs) TODO other files

These [examples](https://github.com/peter-kehl/no_std_rna_slice_patterns) are ordered as they progress:
- [01_on_heap-bytes-own_mut-string](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/01_on_heap-bytes-own_mut-string/src/lib.rs)
- [02_no_heap-chars-own_mut-array-const_overall-limit](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/02_no_heap-chars-own_mut-array-const_overall-limit/src/lib.rs)
- [03_no_heap-array-const_limit-bytes-wipe_on_mut](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/03_no_heap-array-const_limit-bytes-wipe_on_mut/src/lib.rs)
- [04_no_heap-array-const_limit-bytes-wipe_on_clone](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/04_no_heap-array-const_limit-bytes-wipe_on_clone/src/lib.rs)
- [05_no_heap-array-const_limit-bytes-wipe_on_clone-unsafe (*)](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/05_no_heap-array-const_limit-bytes-wipe_on_clone-unsafe/src/lib.rs)
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

(*) `05_no_heap-array-const_limit-bytes-wipe_on_clone-unsafe` (as compared to the previous
implementation) doesn't introduce anything new related to `no_std`, but it fits here. (Also,
`unsafe` is more likely to be used with `no_std` anyway).
---

# Properties of patterns
| Property | [01](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/01_on_heap-bytes-own_mut-string/src/lib.rs "01_on_heap-bytes-own_mut-string") | [02](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/02_no_heap-chars-own_mut-array-const_overall-limit/src/lib.rs "02_no_heap-chars-own_mut-array-const_overall-limit") | [03](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/03_no_heap-bytes-own_mut-array-const_overall-limit/src/lib.rs "03_no_heap-bytes-own_mut-array-const_overall-limit") | [04](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/04_no_heap-bytes-own_mut-array-const_overall-limit-unsafe_str/src/lib.rs "04_no_heap-bytes-own_mut-array-const_overall-limit-unsafe_str") (\*) | [05](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/05_no_heap-bytes-own_mut-array-const_generic-exact/src/lib.rs "05_no_heap-bytes-own_mut-array-const_generic-exact") | [06](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/06_no_heap-bytes-own_mut-array-const_generic-limit/src/lib.rs "06_no_heap-bytes-own_mut-array-const_generic-limit") | [07](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/07_no_heap-bytes-ref_mut-slice-pass_in_storage-mut_anytime/src/lib.rs "07_no_heap-bytes-ref_mut-slice-pass_in_storage-mut_anytime") | [08](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/08_no_heap-bytes-ref_mix-slice-pass_in_storage-mut_initial-macro/src/lib.rs "08_no_heap-bytes-ref_mix-slice-pass_in_storage-mut_initial-macro") | [09](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/09_on_heap-bytes-ref_shr-slice-dispatch_dyn-map/src/lib.rs "09_on_heap-bytes-ref_shr-slice-dispatch_dyn-map") | [10](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/10_no_heap-bytes-ref_shr-slice-dispatch_sta-iterator_enum/src/lib.rs "10_no_heap-bytes-ref_shr-slice-dispatch_sta-iterator_enum") | [11](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/11_no_heap-bytes-ref_shr-slice-dispatch_sta-iterator_impl/src/lib.rs "11_no_heap-bytes-ref_shr-slice-dispatch_sta-iterator_impl") | [12](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/12_no_heap-bytes-ref_shr-slice-dispatch_dyn-eq_branch_iterators/src/lib.rs "12_no_heap-bytes-ref_shr-slice-dispatch_dyn-eq_branch_iterators") | [13](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/13_no_heap-bytes-ref_shr-slice-dispatch_sta-eq_branch_iterators-matrix/src/lib.rs "13_no_heap-bytes-ref_shr-slice-dispatch_sta-eq_branch_iterators-matrix") | [14](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/14_no_heap-bytes-ref_shr-slice-dispatch_sta-eq_iterator_to_generic_fn/src/lib.rs "14_no_heap-bytes-ref_shr-slice-dispatch_sta-eq_iterator_to_generic_fn") | [15](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/15_no_heap-bytes-ref_shr-slice-dispatch_dyn-eq_dispatch_to_specialized/src/lib.rs "15_no_heap-bytes-ref_shr-slice-dispatch_dyn-eq_dispatch_to_specialized") | [16](https://github.com/peter-kehl/no_std_rna_slice_patterns/blob/main/16_no_heap-bytes-ref_shr-slice-dispatch_dyn-eq_dispatch_to_universal/src/lib.rs "16_no_heap-bytes-ref_shr-slice-dispatch_dyn-eq_dispatch_to_universal") |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Implemented | ✓ | ✓ | ✓ | ✓ | ✓ | | part | | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| extra work for securing observability/serialization: array or passed-in mutable slice could leak data! |
| fixed compile-time size limit for all instances (one type) | | ✓ | ✓ | ✓ | | | | | | | | | | | | |
| various compile-time size limits per instance (generic type), can have a default limit | | | | | ✓ | ✓ | | | | | | | | | | |
| no compile-time limit | ✓ |  |  |  |  |  | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| random access & data storage (rather than sequential access only) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |  |  |  |  |  |  |  |  |
| refer to the original (with a lifetime) (rather than copy the original) |  |  |  |  |  |  |  |  | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| refer to extra mutable storage (with a lifetime) |  |  |  |  |  |  | ✓ | ✓ |  |  |  |  |  |  |  |  |
| non-obvious or impractical API (\*) | 05 & 07 & 08 |
| TODO mutable storage at/just before initiation, but then immutable -> shareable? |
| mutable & unlimited resize |
| --> TODO implement mutation for # 01 |
| mutable & limited resize |
| mutable, but no ability to resize |
| immutable |
| extra handling of strings/UTF-8 (\*) |  |  | 🛆 | 🛆 |  | 🛆🛆 | 🛆 | 🛆 |  |  |  |  |  |  |  |  |
| `Clone` is `derive`-d |
| `Clone` is implemented |
| no `Clone` -- needed at all? |
| `Copy` |
| different types for mutation and for sharing: 07 & 08 |
| minor `unsafe` code |
| --- |
|`dyn` (virtual) dispatch <-> static (compile-time) dispatch |
| extra dispatch methods |
| thread safe (`Sync` - if used in `std`) -> TODO "tests": `struct EnsureSync<T: Sync>; type _EnsureSyncRna = EnsureSync<Rna>;` |

- All "unlimited" properties are constrained by available memory.
- (\*) indicates a property or implementation that isn't `no_std`-specific, or is specific to this workspace. It's here for clarification.

TODO Group implementations.
