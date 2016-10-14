# evil-adjust
Adjustments for Emacs end-of-line `eval-` commands in Evil's normal state.


This package compensates for annoying off-by-one incompatibilities between
`evil-normal-state` and lisp modes.

When using `lisp-interaction-mode` in `evil-normal-state`, one cannot use
<kbd>C-x</kbd><kbd>C-j</kbd> (`eval-print-last-sexp`) on the last character of a
sexp, since Emacs thinks the cursor is one space back. This issue usually crops
up when executing the command at the end of the line.

One way of avoiding this is to set the variable `evil-move-cursor-back` to `nil`.
However, this is inconvenient for the majority of commands, since the cursor is
left "hanging over empty space" at the end of the line.

Instead, this package adjusts for the issue by remapping the affected function
to an evil-adjust wrapper: `evil-adjust-eval-print-last-sexp`.

--------------------------------------------------------------------------------

## Emacs 25

With Emacs 25, a similar issue occurs additionally in both `emacs-lisp-mode`
and lisp-interaction-mode when using <kbd>C-x</kbd><kbd>C-e</kbd>
(`eval-last-sexp`).

This is handled by the wrapper `evil-adjust-eval-last-sexp`.

--------------------------------------------------------------------------------

## Installation

* Place `evil-adjust.el` on your emacs `load-path`.
* Add the following initialization code to your `.emacs` or `.emacs.d/init.el`
    file:

        (require 'evil-adjust)
        (evil-adjust)

## Installation (Spacemacs)

* Add the following to `dotspacemacs-additional-packages` in your init file:

        (evil-adjust :location (recipe :fetcher github :repo "troyp/evil-adjust"))

* Add the initialization code (as above) to `dotspacemacs/user-config` in your
    init file.

## Disabling a remapping

If you're on Emacs 25, but don't want to remap `eval-last-sexp` (perhaps the latest
Evil has corrected the problem), you can perform only the `eval-print-last-sexp`
remapping with:

    (evil-adjust :noemacs25fix)

Similarly, `:noevalprintfix` can be used if you *only* want the `eval-last-sexp`
remapping.
