[![Build Status](https://travis-ci.org/leanprover/introduction_to_lean.svg?branch=master)](https://travis-ci.org/leanprover/introduction_to_lean)

An Introduction to Lean
=============

 - Web : https://leanprover.github.io/introduction_to_lean

How to Build
------------

We use [cask][cask] to install emacs dependencies ([org-mode][org-mode], [lean-mode][lean-mode], [htmlize][htmlize]) and [pygments][pygments] and [minted][minted] to syntax-highlight Lean code in LaTeX. We assume that you already have emacs-24.3 or higher installed in your system.

```
sudo apt-get install mercurial python2.7 texlive-latex-recommended \
                     texlive-humanities texlive-xetex texlive-science \
                     texlive-latex-extra texlive-fonts-recommended texlive-luatex\
                     bibtex2html git make mercurial autoconf automake gcc curl \
					 latexmk
git clone https://github.com/leanprover/introduction_to_lean
git clone https://github.com/leanprover/mkleanbook.git

cd introduction_to_lean
make install-cask # after this, you need to add the cask binary to your $PATH
export PATH="$HOME/.cask/bin:$PATH"
make install-pygments
make
```

[cask]: https://github.com/cask/cask
[org-mode]: http://orgmode.org/
[lean-mode]: https://github.com/leanprover/lean/tree/master/src/emacs
[htmlize]: https://github.com/emacsmirror/htmlize
[pygments]: http://pygments.org/
[minted]: https://github.com/gpoore/minted


Automatic Build using Watchman
------------------------------

Using [watchman][watchman], we can detect any changes on the
org-files, and trigger re-builds automatically on the background.

To install [watchman][watchman]:

```
sudo apt-get install automake
make install-watchman
```

To enable watch:

```
make watch-on
```

To disable watch:

```
make watch-off
```

[watchman]: https://github.com/facebook/watchman


How to preview generated HTML files
-----------------------------------

It requires a webserver to preview generated HTML files. We can use Python's `SimpleHTTPServer` module:

```bash
$ python -m SimpleHTTPServer
```

The above command starts a HTTP server at `theorem_proving_in_lean` directory (default port: `8000`). For example, `01_Introduction.html` is available at `http://localhost:8000/01_Introduction.html`.


Auto-reload HTML page
---------------------

 - Firefox: [Auto Reload][firefox-auto-reload] add-on
   - Tools > AutoReload Preferences
![1](https://cloud.githubusercontent.com/assets/403281/4966611/b211cda0-67d5-11e4-876e-a705f3326ac0.png)
   - Create Reload Rule
![2](https://cloud.githubusercontent.com/assets/403281/4966612/b3bdac00-67d5-11e4-83c9-118a4af8b0ea.png)
   - Link .html in the filesystem
![3](https://cloud.githubusercontent.com/assets/403281/4966613/b6461110-67d5-11e4-9d62-93c1e2a8f0da.png)

 - Chrome: [Tincr][google-tincr] (does *not* work on Linux)
   - Right-click and choose "Inspect Element"
![5](https://cloud.githubusercontent.com/assets/403281/5134646/03701bf0-70de-11e4-801f-65f307d30e69.png)
   - Go to "tincr" tab, choose "Http Web Server" for project type, then select Root directory.
![4](https://cloud.githubusercontent.com/assets/403281/5134645/036c6bfe-70de-11e4-86af-c21ec79a4471.png)

[firefox-auto-reload]: https://addons.mozilla.org/en-US/firefox/addon/auto-reload
[google-tincr]: http://tin.cr


Test Lean Code in .org files
----------------------------

 1. Using Native Lean: First, you need to install Lean. Please follow the instructions at the [download page](http://leanprover.github.io/download/). You can test all Lean code blocks in `*.org` files by executing the following command:

    ```bash
make test
    ```

 To use a specific binary of Lean in test, please do the following:
    ```bash
LEAN_BIN=/path/to/your/lean make test
    ```

 2. Using Lean.JS:

    ```bash
make test_js
    ```
