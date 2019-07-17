---
layout: section
order: 3
title: Installation
---

- TOC
{:toc}


## System Requirements

### Stable

- JDK 1.8+
- Emacs 24.5+
- Scala 2.10.6+ / 2.11.11+ / 2.12.3+

### Unstable

- JDK 1.8+
- Emacs 24.5+
- Scala 2.11.11+ / 2.12.3+

## Installing

Note that "stable" means "versioned release jars exist", not "it has less bugs". Indeed, bugs are considered "documented behaviour".

We assume that you already have [MELPA](http://melpa.org) set up as per our [Learning Emacs](/editors/emacs/learning) guide.

The recommended way to install ENSIME is via MELPA stable and `use-package`:

```elisp
(use-package ensime
  :ensure t
  :pin melpa-stable)
```

If you used the sample Emacs configuration from our [Learning Emacs](/editors/emacs/learning) section, then you can add the above code to the end of your `~/.emacs.d/init.el` file and restart Emacs (or `eval-last-sexp`).

If you already installed `ensime` from `melpa` (not `melpa-stable`) using `M-x list-packages`, then you need to delete your `~/.emacs.d/elpa/ensime*` folder, restart Emacs, and follow these instructions.

For the server installation to work, make sure `sbt` is on your `PATH` environment variable or `exec-path` Emacs variable, e.g. on OS X this may mean adding:

```elisp
(add-to-list 'exec-path "/usr/local/bin")
```

or set the sbt command explicitly

```elisp
(setq
  ensime-sbt-command "/path/to/your/sbt.bat"
  sbt:program-name "/path/to/your/sbt.bat")
```

Basic Scala support is provided by [`scala-mode`](/editors/emacs/scala-mode) which provides many features specific to Scala major mode editing and sbt support is provided by [`sbt-mode`](/editors/emacs/sbt-mode). Both modes can be used independently of ENSIME and you are encouraged to read their standalone documentation to understand the role that they play.

## Unstable Edition

Note that "unstable" means "it does not have versioned releases", not "it will crash a lot". You are expected to fix bugs you encounter.

To use the unstable version of ENSIME from MELPA, change to `:pin melpa`:

```elisp
(use-package ensime
  :ensure t
  :pin melpa)

(use-package sbt-mode
  :pin melpa)

(use-package scala-mode
  :pin melpa)
```

and read the documentation for your build tool plugin (which is now the server installer) for additional steps that you need to make.

Note that the ensime-server `3.0.0-SNAPSHOT` releases are incompatible with the emacs client, blocked by [use SWANKY](https://github.com/ensime/ensime-emacs/issues/316).

## Spacemacs

We would rather that you used stock Emacs with `evil-mode`. However, if you still choose to use Spacemacs, you must add these lines to your `dotspacemacs/user-init` to mimic the configuration above.

```elisp
(push '("melpa-stable" . "stable.melpa.org/packages/") configuration-layer-elpa-archives)
(push '("ensime" . "melpa-stable") package-pinned-packages)
```

Please do not raise bug reports unless you can reproduce with stock Emacs, because none of the core contributors use or understand Spacemacs.


## Starting

Compile your project with your [build tool](/build_tools) and generate a `.ensime` file (which also installs / updates the server component). Then navigate to a file or directory in your project and type:

```
M-x ensime
```

**Check that again**. It is very important that you compile your project and have generated a `.ensime` file from one of the supported build tools.

The first time you use ENSIME, you can expect to wait several minutes for the server and all of its dependencies to be downloaded.

On first use for a project, you will need to wait a few moments for indexing to complete.

Once the server is available, enjoy editing with the ENSIME commands that are documented in the [User Guide](/editors/emacs/userguide) and consider using some of the suggestions in our [Hacks](/editors/emacs/hacks) page to improve your productivity in Emacs when editing Scala code.
