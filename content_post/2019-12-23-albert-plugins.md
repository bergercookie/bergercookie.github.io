---
author: bergercookie
categories:
- programming
- linux
- tooling
comments: true
date: "2019-12-23T15:28:00Z"
draft: false
title: Using Albert to boost your productivity
---

I've lately been very active developing plugins for the
[Albert](https://albertlauncher.github.io/) launcher for many parts of my daily
routine.
For those of you that don't know it, Albert is an application launcher for
Linux. It's written in C++ and its GUI is built on top of Qt. The current post
is a short summary of the plugins I've implemented to automate parts of my
current routine and maximise my productivity along with advise and, hopefully,
useful information on how to do the same for your needs via Albert.

If you want to extend Albert's capabilities you basically have two options:

- Implement a native Albert plugin in C++. For this you have to clone the
  Albert repository, implement and compile your plugin along with the overall
  repo.
- Alternatively you can write a [python
  extension](https://albertlauncher.github.io/docs/extensions/python/). The
  latter can be developed separately from the main Albert repo and can be
  enabled/disabled via an option in the application settings. This goes
  without saying that, if you're comfortable with Python and you're willing to
  sacrifice a tiny bit of performance when the plugin is running, then this
  should be your go-to choice.

In my case, I followed the latter approach and in the last ~3 months I implemented a
series of plugins to automate parts of my daily routine. All the plugins as well
as the overall content of this article can be found in the
[awesome-albert-plugins
repo](https://github.com/bergercookie/awesome-albert-plugins). Following is a
list of the plugins I implemented, along with a short description of what each
plugin does:

- [Jira](https://www.atlassian.com/software/jira): Mark tickets as in-progress/under-code-review/done, do fuzzy search on
  their title, navigate to the corresponding ticket page
- [Taskwarrior](https://taskwarrior.org/): Interact with taskwarrior - fuzzy search on title, change status
  of task
- [Zoopla](https://www.zoopla.co.uk/) - Search Property to Buy, Rent, House Prices
- [Xkcd](https://xkcd.com/) - Fetch xkcd comics  - do fuzzy search on title
- [Google Maps](https://maps.google.com) - Fetch instructions from/to a specific place, optionally via
  specific transportation means
- Suggestions-enabled search for various websites using
    [googler](https://github.com/jarun/googler). For example:

    Google
    Amazon
    Youtube
    Github
    Ebay
    IMDB
    ...


Here are some demo pictures of these plugins:

| ![](/images/albert-demos/albert-suggestions-demo2.gif) | ![](/images/albert-demos/albert-suggestions-demo.gif) |
|:---:|:---:|
| ![](/images/albert-demos/albert-suggestions-demo3.gif) | ![](/images/albert-demos/taskwarrior-demo.gif) |
| ![](/images/albert-demos/xkcd-demo.gif) | ![](/images/albert-demos/youtube-demo.gif) |

<br/>

<center>
<img src="/images/albert-demos/demo-fuzzy-search-title.png">
<br/>
Do a fuzzy search of your assigned JIRA tickets
</center>

<br/>

<center>
<img src="/images/albert-demos/search_plugins.png">
<br/>
View of many suggestions-enabled saerch plugins
</center>

Since I spent a good deal of time writing these plugins, I figured I could share
some of my conclusions, shortcuts into writing a new plugin for your own
usecases:

- Use [cookiecutter](https://cookiecutter.readthedocs.io/en/latest/) to minimise
  the boilerplate code for your new plugin. The former uses the
  [Jinja](https://www.palletsprojects.com/p/jinja/) templating language to
  substitute placeholder values in the contents of files and in the names of the
  files and directories.
  Here's the [cookiecutter
  package](https://github.com/bergercookie/awesome-albert-plugins/tree/master/cookiecutter)
  layout that I have been using for spawning new Albert plugins:

  {{< highlight sh >}}
    cookiecutter/
    ├── cookiecutter.json
  ├── {{cookiecutter.plugin_name}}
    │   ├── __init__.py
    │   ├── install-plugin.sh
    │   ├── misc
    │   │   └── demo.gif
    │   └── README.md
    └── README.md
  {{< / highlight >}}

  And here are the modifiable variables when creating a new plugin:

  {{< highlight json "linenos=table" >}}
  {
      "author": "Nikos Koukis",
      "plugin_name": "albert_plugin",
      "parent_repo_url": "https://github.com/bergercookie/awesome-albert-plugins",
      "repo_base_url": "https://github.com/bergercookie/awesome-albert-plugins/blob/master/plugins/",
      "download_url_base": "https://raw.githubusercontent.com/bergercookie/awesome-albert-plugins/master/plugins/{{ cookiecutter.plugin_name }}/",
      "plugin_short_description": "Some title for your plugin",
      "albert_plugin_interface": "v0.2",
      "version": "0.1.0"
  }
  {{< / highlight >}}

- Give the user an easy way of raising issues and bugs

  When using an albert plugin (or a general-purpose python script) many things
  can go wrong at runtime (HTTP connection errors, filesystem errors etc.).
  Moreover, the potential plugin user may be running albert on the background,
  without having access to the corresponding pseudoterminal it was launched
  from. This is why, in case of an error, the plugin will silently fail. Here's
  a snippet of code that I've been using so that errors are not left unnoticed
  as well as an easy way for the user to report the bug:

  {{< highlight python "linenos=table" >}}
  import traceback

  if query.isTriggered:
      try:
          # whatever your pugin does goes here
          # ...
      except Exception:  # user to report error
          results.insert(
              0,
              v0.Item(
                  id=__prettyname__,
                  icon=icon_path,
                  text="Something went wrong! Press [ENTER] to copy error and report it",
                  actions=[
                      v0.ClipAction(
                          f"Copy error - report it to {__homepage__[8:]}",
                          f"{traceback.format_exc()}",
                      )
                  ],
              ),
          )

    return results
  {{< / highlight >}}

  Now, in case an exception is raised during runtime, the user is greeted with
  the following message:

  ![albert-error-message](/images/albet-plugin-error-msg.png)

  And when pressing ENTER, the appropriate ISSUES page URL is copied to the
  clipboard.

- Have a setup phase for checking that all the requirements for your plugin are
  in place

  In case more setup steps are required (e.g., login credentials)  that can
  happen as part of the first albert plugin run(s). In my case, I've been using
  a `setup` function called at the start of the plugin that checks that all the
  requirements are in-place before actually going through the main plugin
  functionality. Here's a sample of how the setup phase works for the JIRA
  plugin:

  {{< highlight python "linenos=table" >}}
  if query.isTriggered:
      try:
          results_setup = setup(query)
          if results_setup:
              return results_setup
          # setup OK.

          user = load_data("user")
          server = load_data("server")
          api_key = load_api_key()

  ...

  def setup():
    results = []

    if not shutil.which("pass"):
        results.append(
            v0.Item(
                id=__prettyname__,
                icon=icon_path,
                text=f'"pass" is not installed.',
                subtext='Please install and configure "pass" accordingly.',
                actions=[
                    v0.UrlAction('Open "pass" website', "https://www.passwordstore.org/")
                ],
            )
        )
        return results

    # user
    if not user_path.is_file():
        results.append(
            v0.Item(
                id=__prettyname__,
                icon=icon_path,
                text=f"Please specify your email address for JIRA",
                subtext="Fill and press [ENTER]",
                actions=[v0.FuncAction("Save user", lambda: save_data(query.string, "user"))],
            )
        )
        return results

    # password (same for API key)
    if not server_path.is_file():
        results.append(
            v0.Item(
                id=__prettyname__,
                icon=icon_path,
                text=f"Please specify the JIRA server to connect to",
                subtext="Fill and press [ENTER]",
                actions=[
                    v0.FuncAction(
                        "Save JIRA server", lambda: save_data(query.string, "server")
                    )
                ],
            )
        )
        return results

  # ...
  def save_data(data: str, data_name: str):
      """Save a piece of data in the configuration directory."""
      with open(config_path / data_name, "w") as f:
          f.write(data)


  def load_data(data_name) -> str:
      """Load a piece of data from the configuration directory."""
      with open(config_path / data_name, "r") as f:
          data = f.readline().strip().split()[0]

      return data

  {{< / highlight >}}

  Thus, in this case, on the fist run, the user will have to write their
  username and server on the albert prompt, which will be saved in appropriate
  files, and in the following 2 plugin runs, the plugin will check that their
  password and API key can be appropriately found using the Pass
  password manager.

- Give the user an easy way of installing the plugin.

  Along with each new albert plugin, I've been adding (again generating it via
  cookiecutter) an `install-plugin.sh` script that sets up all the plugin
  dependencies via either the system package manager (e.g., `apt-get`) or the
  language package manager
  (i.e., `pip`) and also copies the plugin directory to the local albert modules
  installation, i.e.: `~/.local/share/albert/org.albert.extension.python/`.

That's all for now. Let me know if this has been helpful or has given you any
inspiration for making your own extensions.
