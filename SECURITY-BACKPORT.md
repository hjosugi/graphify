# Fortran preprocessing security backport

GHSA-pcc4-rvhr-2pr8 is fixed locally using the source and regression tests from
[upstream commit e1d9deed](https://github.com/Graphify-Labs/graphify/commit/e1d9deed6a437f2c85458ef3c42519159f322b7b).
The project version remains 0.9.31; version-only scanners will still report it.

Additional handling uses the existing raw-source fallback for C comments,
line splicing, digraphs/trigraphs, pragmas, and filesystem-probing builtins.
Normal macro/conditional preprocessing remains available. Include, include_next,
import and embed directives are removed before invoking cpp on standard input.
Ambiguous source is parsed without preprocessing; it cannot cause cpp to read
host files. Regression tests cover alternate directive spellings as well as
ordinary absolute, relative and same-directory includes.

Retire this backport after merging a reviewed upstream security release that
also handles these alternate directive forms.

The supported Python minimum is 3.11 so the universal lock can resolve the fixed Filelock and Pillow releases; Python 3.10 cannot install these fixes. Other package versions are updated selectively to preserve the tested parser grammar versions.
