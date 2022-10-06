# Scope

- Primary focus: Memory handling.

TODO
- beware that vscode.dev can't display inferred types (of `let` definitions), neither declared
  parameter names in function calls
- vote for [enabling rust-analyzer on vscode.dev](https://github.com/rust-lang/rust-analyzer/issues/11309)
- https://github.dev/peter-kehl/no_std_rna_slice_patterns
  - VS-Code-like horizontal menu (if you have it hidden by default, toggle it with "Alt")
  - your VS Code theme (if you use VS Code sync)
  - `Ctrl + comma` shows VS-Code-like Settings
- Alternative: Online VS Code:
 - https://vscode.dev/github/peter-kehl/no_std_rna_slice_patterns
 - [Insiders (beta-like version)](https://insiders.vscode.dev/github/peter-kehl/no_std_rna_slice_patterns)
 - these don't have a horizontal menu, but open it by the hamburger button

---
# Prerequisites

- `nightly` Rust compiler
 - the actual solutions work with `stable` Rust. However, the test harness (with extras on top of of
   Exercism's tests) needs `nightly` Rust (as of mid 2022).

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

TODO Group implementations?

---

# Methods

# no_std with heap

Replace use of `HashSet/HashMap` with `BTreeSet/BTreeMap` when possible. Or create different data
structures. Or use 3rd party crates.

Replace `Arc` with `Rc` (since there is no multi-threading in `no_std`).

# no_std without heap

- Have your functions accept [slices](https://doc.rust-lang.org/nightly/book/ch04-03-slices.html)
   (shared or mutable), rather than `Vec` or `String`, wherever possible. Both `Vec` and `String`
   auto cast/expose themselves as a slice. (This is a good practice even with heap, or in `std`.)
- Similarly, whenever possible, have your `struct`-s and `enum`-s store references, or slices,
   rather than own the data. It does involve
   [`lifetimes`](https://www.cloudbees.com/blog/lifetimes-in-rust), but that can be a good practice,
   too.

- Can't
   [`core::iter::Iterator.collect()`](https://doc.rust-lang.org/core/iter/trait.Iterator.html#method.collect).
  - Even though `collect()` does exist in `core` (and not only in `std`), it can collect only to
   implementations of
   [`core::iter::FromIterator`](https://doc.rust-lang.org/core/iter/trait.FromIterator.html). (That,
   again, exists in `core`, in addition to `std`). However, there are no `core`-only implementors of
   `FromIterator` (other than collecting zero or one item [to
   `core::option::Option`](https://doc.rust-lang.org/core/iter/trait.FromIterator.html#impl-FromIterator%3COption%3CA%3E%3E)
   or [to
   `core::result::Result`](https://doc.rust-lang.org/core/iter/trait.FromIterator.html#impl-FromIterator%3CResult%3CA%2C%20E%3E%3E)).
  - `collect()` doesn't exist for arrays nor slices (without heap). Hence we need to iterate and
   store in a (mutable) array or slice.  _New to Rust? And Worried about side effects?_ Good news:
   _Safe_ Rust prevents unintended side effects, because we "[cannot have a mutable reference while
   we have an immutable
   one](https://doc.rust-lang.org/nightly/book/ch04-02-references-and-borrowing.html#mutable-references)
   to the same value."
- there is no dynamic/resizable data storage
  - a `no_std` design needs to batch/buffer/limit the total data
  - use slices (instead of arrays) as parameter types wherever possible
    - design function as accepting (shared or mutable) slices
    - functions may need to write to mutable slice parameters  (instead of returning).

---

- _New to Rust?_ Mutating slices or references/arrays may sound less "functional". But, in Rust any
     mutated parameters must be declared so. Any parameter that may be modified must be either
  - [`borrowed`](https://doc.rust-lang.org/nightly/book/ch04-02-references-and-borrowing.html)
       (passed) as a mutable reference or slice (which has exclusive access), or
  - passing ownership of the object:
    - [_"move"-d_](https://doc.rust-lang.org/nightly/book/ch04-01-what-is-ownership.html#ownership-and-functions)
         (or [`clone()`-d](https://doc.rust-lang.org/core/clone/trait.Clone.html) first and then the
         clone is moved), or
    - [_copied_: Ownership > Stack-Only Data: Copy]
         ](<https://doc.rust-lang.org/nightly/book/ch04-01-what-is-ownership.html#stack-only-data-copy>)
         if it implements [`Copy` ](https://doc.rust-lang.org/core/marker/trait.Copy.html) trait.
         _New to Rust?_ A `trait` is similar to an `interface` in Java, a `virtual` abstract
         field-less class with virtual methods in C++, or a `protocol` in some other languages.
  - See also
       [ownership](https://doc.rust-lang.org/nightly/book/ch04-00-understanding-ownership.html),
       [borrowing](https://doc.rust-lang.org/nightly/book/ch04-02-references-and-borrowing.html) and
       [lifetimes](https://doc.rust-lang.org/nightly/book/ch10-03-lifetime-syntax.html).
- alternatively, use [`const` generics](https://rust-lang.github.io/rfcs/2000-const-generics.html),
     a subset of Rust [generics](https://doc.rust-lang.org/nightly/book/ch10-00-generics.html), for
     both function parameters and return values
  - make the array size (which has to be known in compile time) a `const` generic parameter
  - beware that generics make the executable larger, and the build process takes longer; it helps to
       combine (`const`) generics for some functions, and slices for other
- application's top level function(s) define the array(s), or array-containing structs/enums, on
     stack. Then they call the processing functions with slices, or with const generic-sized arrays
     (or their references)

---

- this way you can re-use the same processing functions
- if you can process the incoming data last in, first out (in LIFO/stack order), you could recurse
     (possibly batching the data in an array at every recursion level)
- Have functions return an iterator wherever possible. (And use it for parameters, too. Again, a
   good practice even in `std`.)
  - may need to implement
     [core::iter::Iterator](https://doc.rust-lang.org/core/iter/trait.Iterator.html) to represents
     results of your transformation. Such iterators refer to the underlying iterator (data
     source/origin) and they may keep some state on top of it (a state machine).
  - You may want to combine/chain functions accepting and returning iterators. Use keyword
     [`impl`](https://doc.rust-lang.org/nightly/book/ch10-02-traits.html#returning-types-that-implement-traits)
     to define types like `impl Iterator<Item = YourItemType>`.

---

# no_std without heap > Alternatives to collect()

When developing for `no_heap`, we can't `collect()` from iterators. That makes some tasks that need
random access (access to all items at the same time, like sorting) difficult.

This would need limit on number of items to be known at build time. Then the caller would pass a
(mutable) reference to an array, or a slice, where we would manually collect the items (in a `for`
loop, or `.foreach()` closure).

---

# no_std without heap > Compound iterators

For some purposes we may not need access to all items if we don't need to access the whole
collection. Then all we do needs sequential access only, for example a one-to-one transformation,
and/or filtering.

For that we may need to implement a compound iterator. It would contain an underlying iterator (or
several iterators) over the source data. It iterates and transforms and/or filters the source data.

[Exercism Rust track](https://exercism.org/tracks/rust/exercises) > [RNA
Transcription](https://exercism.org/tracks/rust/exercises/rna-transcription)

In addition to the text of the assignment, it helps to see the
[tests](https://github.com/peter-kehl/x-rust/blob/main/rust/rna-transcription-std/tests/rna-transcription.rs)
(or the same tests used for [`no_std`
version](https://github.com/peter-kehl/x-rust/blob/main/rust/rna-transcription-no_std-no_heap/tests/rna-transcription.rs))

<https://github.com/peter-kehl/x-rust/blob/main/rust/rna-transcription-std/src/lib.rs>

<https://github.com/peter-kehl/x-rust/blob/main/rust/rna-transcription-no_std-no_heap/src/lib.rs>
