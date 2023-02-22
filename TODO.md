# TODOs:

-   BUG: `(a / b) / (c / d)` turns into `ac / (bd)`, but it should turn into `ad / (bc)`
-   `a + a` should be turned into `2 * a`. This gets more complicated because `2 * a + a` should turn into `3 * a` and subtractions should be considered too.
-   The above todo should also be applicable to `*`, `/` and `**`. Having some abstract rules for it would be useful.
-   Accept prettified strings. Specifically `3a` should be tokenized like `3 * a`
    -   How to deal with multi-character variables? Should `ab` be read as two different names or as one name?
    -   Maybe assume names to always be single characters except for capitalized strings?
-   Let user write their own functions with their own rules
