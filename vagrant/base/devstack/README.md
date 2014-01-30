# Baseline Vagrant Development

To develop a product from Open edX, you will want to accomplish a couple of things:

* select a stable starting point;
* fork to your product directory;
* package a starting point vagrant box to ease development;
* add product specific theme(s);
* add product specific environment;
* triage against a known system;
* develop and test against branch variants;
* ... and more;

For this, start by building an Open edX version you find works, feel comfortable with.
You can build this starting point yourself.

For example, fork the Open edX repositories you plan to use.
Identify a specific release or version, and build a box against it.
Optionally create a branch for your product, and identify it
in the `build_version.json` configuration file.
You may choose to use some components without modification
from the Open edX repositories.
If so, be sure to mark their version.
It's not recommended to tag repositories not under your
control (e.g. Open edX ones) as `HEAD` or `master` since
over time your product can potentially become unstable.
Instead, select the tag or version for your repository
(you can get a commit # with, e.g., `git rev-list -n 1 master`).

Copy `build_version.json.template` to `build_version.json`
and edit the appropriate fields.
You will not use all the components which you
can specify repositories and versions for - omit what you
don't need.

These ansible variables will override their settings in
the playbooks.

See the `ansible.extra_vars` option of
[http://docs.vagrantup.com/v2/provisioning/ansible.html](http://docs.vagrantup.com/v2/provisioning/ansible.html)
for more info.

Here is an example of variables currently used in Open edX
playbooks.

A canonical theme, used as a starting point, comes from
[https://github.com/Stanford-Online/edx-theme](https://github.com/Stanford-Online/edx-theme).
You can point your theme account to your `GIT_ACCT`,
or some other other account, once you've confirmed
that the alternate theme from Stanford builds.

```
	{
	    GIT_ACCT: "Your_Github_Account_Here",
	    THEME_ACCT: "Stanford-Online",
	    OPEN_EDX: "edx",
	    edx_platform_repo: "https://{{ COMMON_GIT_MIRROR }}/{{ GIT_ACCT }}/edx-platform.git",
	    edx_platform_version: "stable/theme-2014-01-20",
	    forum_source_repo: "https://{{ COMMON_GIT_MIRROR }}/{{ GIT_ACCT }}/cs_comments_service.git",
	    forum_version: "stable/theme-2014-01-20",
	    ora_source_repo: "https://{{ COMMON_GIT_MIRROR }}/{{ OPEN_EDX }}/edx-ora.git",
	    ora_version: 'master',
	    ora_ease_source_repo: "https://{{ COMMON_GIT_MIRROR }}/{{ OPEN_EDX }}/ease.git",
	    ora_ease_version: 'master',
	    edxapp_use_custom_theme: true,
	    edxapp_theme_source_repo: 'https://{{ COMMON_GIT_MIRROR }}/{{ THEME_ACCT }}/edx-theme.git',
	    edxapp_theme_version: 'HEAD',
	    edxapp_theme_name: "stanford"
	}
```


