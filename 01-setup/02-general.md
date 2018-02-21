# General Tools

## Package Manager

First things first, you'll want to install a package manager to make installing all the required tools easy. Package managers include a series of commands that automate installing, upgrading, and removing programs in a simple and consistent manner. The package manager you should install depends on the operating system you're using. If you're on ubuntu and debian, you already have the `apt-get` library built in. For OS X, you'll need to install [Homebrew](http://brew.sh).

Each package manager will typically follow the same pattern for its commands. In the following examples, we'll use apt-get:
- `apt-get install package` - searches and attempts to install the given package name. Packages can be chained after another, e.g. apt-get install package1 package2 will install package1 and package2.
- `apt-get update` - updates the internal source listing, i.e. package listings.
- `apt-get upgrade` - takes the currently installed packages and checks for any newer versions and installs them.
- `apt-get remove package` - removes the given package name.
- `apt-get autoremove` - cleans up dependencies that are no longer being used.

### Homebrew (OS X)

To install homebrew, you'll first need to install Xcode Command Line Tools.

```sh
xcode-select --install
```

Next, install homebrew.

```sh
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

## Git

We use Git for source control to host our code and make collaboration easy. It allows us to work on multiple versions of thecourseforum at a time and to manage changes easily. Use your package manager to install git.

```sh
apt-get install git
```
or
```sh
brew install git
```

## Postman

[Postman](https://www.getpostman.com/) is a useful tool to try out http requests for different endpoints on the site. It'll make testing endpoints incredibly easy.

## Text Editor

It's up to you how you want to develop and write code. There are two main text editors -- [Sublime Text](https://www.sublimetext.com/) and [Atom](https://atom.io/) -- which are probably your best bet. They are great environments for editing code and also have numerous plugins which add even more functionality. Your other options are terminal editors such as vim, nano, and emacs. vim is probably the most ubiquitous option out there; however, it has a rather steep learning curve. It has powerful shortcuts and extensive customization that make it a favorite of more experienced developers. The choice is up to you -- though let us know if you want to try out vim so we can help you with setup!

[Next &raquo; Dependency Installation](/01-setup/03-dependencies.md)
