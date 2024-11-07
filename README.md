Haskell completion source for Emacs auto-complete package
=========================================================

This plugin provides a completion source for the popular Emacs
interactive auto-completion framework
[auto-complete](http://cx4a.org/software/auto-complete/). Completions
are taken from the current background Haskell process managed by
`haskell-mode`.

**Latest stable version**: see the
[latest numbered tag](https://github.com/purcell/ac-haskell-process/tags),
which will also be the latest version available via MELPA Stable.

Installation
=============

First, ensure `auto-complete` and `haskell-mode` are installed: I recommend
using packages from [Melpa][melpa].

You'll need both `auto-complete` and `haskell-mode` to be enabled and
working, so please consult the corresponding documentation if you have
any trouble with this.

Next, install `ac-haskell-process`. If you choose not to use the convenient
package in [Melpa][melpa], you'll need to
add the directory containing `ac-haskell-process.el` to your `load-path`, and
then `(require 'ac-haskell-process)`.

To enable the completion source this, put the following code in your
emacs init file:

```el
(require 'ac-haskell-process) ; if not installed via package.el
(add-hook 'interactive-haskell-mode-hook 'ac-haskell-process-setup)
(add-hook 'haskell-interactive-mode-hook 'ac-haskell-process-setup)
(eval-after-load "auto-complete"
  '(add-to-list 'ac-modes 'haskell-interactive-mode))
```

If you want to trigger `auto-complete` using <kbd>TAB</kbd> in REPL buffers, you may
want to put `auto-complete` into your `completion-at-point-functions`:

```el
(defun set-auto-complete-as-completion-at-point-function ()
  (add-to-list 'completion-at-point-functions 'auto-complete))
(add-hook 'auto-complete-mode-hook 'set-auto-complete-as-completion-at-point-function)
(add-to-list 'ac-modes 'haskell-interactive-mode)
(add-hook 'haskell-interactive-mode-hook 'set-auto-complete-as-completion-at-point-function)
(add-hook 'haskell-mode-hook 'set-auto-complete-as-completion-at-point-function)
```

You can use `ac-haskell-process-popup-doc` to pop up documentation
for the symbol at point:

```el
(eval-after-load 'haskell-mode
  '(define-key haskell-mode-map (kbd "C-c C-d") 'ac-haskell-process-popup-doc))
```

This currently requires that Emacs can execute the "hoogle" command.

Usage
=====

`ac-haskell-process` should now automatically be enabled when you
visit a buffer in which `interactive-haskell-mode` is active and
`auto-complete` is enabled. (Check the modeline.)

Simply trigger auto-completion, and completion candidates supplied by
nrepl should be displayed, with the symbol "h" on the right hand side of the
completion pop-up to indicate that the completion was provided by this source.
After a short delay, popup
documentation for the completed symbol should also be displayed.


[melpa]: http://melpa.org

Acknowledgements
================

`ac-haskell-process` was written by [Steve Purcell](https://github.com/purcell).

<hr>

[💝 Support this project and my other Open Source work via Patreon](https://www.patreon.com/sanityinc)

[💼 LinkedIn profile](https://uk.linkedin.com/in/stevepurcell)

[✍ sanityinc.com](http://www.sanityinc.com/)
