## 1. What is it?

Repository with unofficial [**HTML Tidy**](https://www.html-tidy.org/) [**release 5.9.20**](https://github.com/Kristinita/tidy-html5/releases). Use binaries from this release as you used binaries from official releases.

## 2. Why it was created?

The latest official Tidy [**stable release 5.8.0**](https://github.com/htacg/tidy-html5/releases/tag/5.8.0) and [**pre-release 5.9.14-next**](https://github.com/htacg/tidy-html5/releases/tag/5.9.14-next) contains the critical bug — [**they remove line breaks inside `<pre></pre>` tags**](https://github.com/htacg/tidy-html5/issues/1006#issuecomment-1246422318). This bug [**fixed by the pull request #1117**](https://github.com/htacg/tidy-html5/pull/1117), but the pull request isn’t approved, because HTML Tidy [**unmaintained since January 2022**](https://github.com/htacg/tidy-html5/commits/next/).

The previous official release 5.6.0 doesn’t contain this bug, but Tidy developers [**doesn’t release 5.6.0 binaries for Linux**](https://github.com/htacg/tidy-html5/releases/tag/5.6.0). The penultimate official release 5.4.0 contains some problems.

Because I haven’t found an alternative to Tidy that fixes problems in HTML files, I decided to make an unofficial HTML Tidy release that would include a fix from pull request #1117 and features from the [**branch `next`**](https://github.com/htacg/tidy-html5/commits/next/) of the official Tidy repository.

## 3. How to use Tidy from this release?

### 3.1. Manual downloading and placing binaries

URL of UNIX binary:

```text
https://github.com/Kristinita/tidy-html5/releases/download/5.9.20/tidy
```

URL of Windows binary:

```text
https://github.com/Kristinita/tidy-html5/releases/download/5.9.20/tidy.exe
```

Download binary file for your operating system → place the binary file to the directory included to PATH of your operating system or virtual environment → use Tidy as usual.

### 3.2. gh-release-install

I use Python package [**gh-release-install**](https://github.com/jooola/gh-release-install) for downloading and placing binaries from GitHub releases.

For example, I use [**Pipenv**](https://pipenv.pypa.io/en/latest/) for my Python projects. I placed Tidy binaries to the Pipenv directories for binaries — `.venv/bin` for UNIX and `.venv/Scripts` for Windows.

UNIX command:

```shell
gh-release-install Kristinita/tidy-html5 tidy .venv/bin --verbose
```

Windows command:

```shell
gh-release-install Kristinita/tidy-html5 tidy.exe .venv/Scripts --verbose
```

Check whether Tidy is running:

```shell
pipenv run tidy --version
```

HTML Tidy must successfully run on [**UNIX**](https://app.travis-ci.com/github/Kristinita/SashaTravis/builds/274563821#L248) and [**Windows**](https://ci.appveyor.com/project/Kristinita/sashatravis#L72).

```shell
pipenv run tidy --version
HTML Tidy for Windows version 5.9.20
```

## 4. How binaries were compiled?

I followed [**instructions from the official HTML Tidy repository**](https://github.com/htacg/tidy-html5/blob/next/README/BUILD.md).

I compiled the UNIX binary on the Travis CI, see [**the build for details**](https://app.travis-ci.com/github/Kristinita/tidy-html5/builds/274563864).

I compiled the Windows binary on the AppVeyor CI, see [**the build for details**](https://ci.appveyor.com/project/Kristinita/tidy-html5/builds/51702673).

## 5. Testing

I tested the command `tidy -modify` on my real project, and visually I can’t find any problems in HTML Markup caused by Tidy. I checked modified HTML files use HTML Tidy, the official [**Nu Html Checker**](https://github.com/validator/grunt-html), [**HTMLLint**](https://github.com/htmllint/htmllint/wiki) and [**HTMLHint**](https://htmlhint.com/) — all these tools returned, that my HTML files are valid.

I tested binaries from my release on Windows and Ubuntu. I never use macOS in my life, and I don’t know, is binary from this release works correctly on this operating system. Please let me know or better yet, send a pull request, if Tidy from this release works incorrectly on macOS.
