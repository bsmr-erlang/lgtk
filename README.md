# ℓGTK

*An LFE GTK 2.0 API that wraps the Erlang gtknode library*

[![][lgtk-logo]][lgtk-logo-large]

[lgtk-logo]: resources/images/lGTK-logo.png
[lgtk-logo-large]: resources/images/lGTK-logo-large.png


#### Contents

* [Introduction](#introduction-)
  * [ℓGTK vs. gtknode](#ℓgtk-vs-gtknode-)
  * [Modules](#modules-)
  * [Caveat](#caveat-)
* [Dependencies](#dependencies-)
* [Building](#building-)
* [Usage](#usage-)
* [Documentation](#documentation-)


## Introduction [&#x219F;](#contents)

As odd as it may seem, LFE and GTK are actually a very good combination. LFE is a language that runs on a VM that was built to support highly-concurrent communications betewen native (Erlang/BEAM) and non-native (Ports) code. Due to its inherent message passing, LFE supports asynchronous calls. In addition to generic software servers, LFE also supports event servers -- both are useful integrating with GUI main loops and managing signals. Furthermore, due to LFE's support of distribution, it is possible to create GTK GUIs that manage or interact with light-weight language processes that run on multiple cores or even on remote systems.


### ℓGTK vs. gtknode [&#x219F;](#contents)

Or: *Why create a wrapper?* The answer to this is quite simple: though the use of gtknode is very elegant and simple (espcially if you have long experience in the Erlang world), the approach is not very Lisp-y. Additionally, if you *don't* come from the Erlang world, the use of gtknode in LFE will seem quite strange.

Here is an example call using gtknode:

```cl
(! name `#(,(self) (#(Gtk_statusbar_push `(statusbar1 ,sb-stx-id "Connected"))))
(receive
 (`#(,name #(reply (#(ok ,rep)y))))
 reply)
```

Here is the same call in ℓGTK:

```cl
(gtk.statusbar:push name 'statusbar1 sb-ctx-id "Connected")
```

This library attempts to provide LFE hackers with a natural-feeling API (one that closely mirros the APIs in other GTK language bindings) for creating GTK apps that run on the Erlang VM.


### Modules [&#x219F;](#contents)

ℓGTK modules are named using a "dotted" notation that is meant to provide a context to the developer; there are no such things as packages or sub-packages in LFE or Erlang, so this notatation does not signify any underlying structure.

ℓGTK modules are grouped into the following, by name:

* <strong>gtk.*</strong> modules - These correlate directly to GTK+ classes
* <strong>gn.*</strong> modules - These are wrappers for gtknode-specific functions
* <strong>lgtk.*</strong> modules - These are ℓGTK-specific functions (e.g., the ``gen_server``)


### Caveat [&#x219F;](#contents)

**Here there be dragons!** This library is a work in progress, with nowhere near complete support of the GTK 2.0 API. That being said, adding new functions is *mostly* a trivial exercise; if you are comfortable with the source code, you may enjoy submitting patches that add support for your favourite missing GTK functions.


## Dependencies [&#x219F;](#contents)

ℓGTK has the following system dependencies:

* Erlang
* ``rebar``
* GNU ``make``
* ``libglade2`` and its development files

If you would like to use the dark theme included in ``priv``, you will also need:

* ``gtk2-engines``
* ``gtk2-engines-pixbuf``

Erlang and LFE-specific dependencies will be downloaded automatically when running ``make``.


## Building [&#x219F;](#contents)

Simply run the following in your ``clone``d directory (after you have the system dependencies installed):
```bash
$ make
```

This will:

1. Download all the dependencies
1. Compile source (as well as that of its dependencies), and
1. Bring up a GTK window.


## Usage [&#x219F;](#contents)

TBD


## Documentation [&#x219F;](#contents)

There are two sources of documentation -- both also works in progress -- for ℓGTK:

* The [LFE GTK example project](https://github.com/oubiwann/lfe-gtknode-example) repo
* The [ℓGTK Tutorial](https://lfe.gitbooks.io/gtk2-tutorial/content/) GitBook
