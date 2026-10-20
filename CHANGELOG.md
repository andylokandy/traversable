# CHANGELOG

All notable changes to this project will be documented in this file.

## Unreleased

### Breaking changes

* Visitor enter methods return `ControlFlow<Break, Continue>`; handwritten traversal implementations must honor `Continue::Skip`. Enter closure factories accept an additional continuation type parameter.

* Type-level `#[traverse(skip)]` is no longer supported. Use `#[traverse(skip_self)]` to skip calling the visitor for the annotated struct or enum while still traversing its children.

### New features

* Skip a subtree at runtime with `Continue::Skip`, without stopping sibling traversal.
* Carry per-node state with `visitor_events` and `visitor_events_mut`, or the enter-only `visitor_enter_scoped` and `visitor_enter_scoped_mut` (requires `std`). Callbacks can return `Continue` directly or `ControlFlow` for early termination.

* Add type-level `#[traverse(skip_self)]` and `#[traverse(skip_children)]` attributes for structs and enums.
* `#[traverse(skip_children)]` skips traversing the children of the annotated struct or enum, but still calls the visitor for it, unless `#[traverse(skip_self)]` is also present.
