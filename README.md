# cloudbleed-browser-scan

This script is designed to make it easy to scan your browser history
to search for sites potentially affected by CloudBleed.

Currently there is a massive list of CloudFlare-enabled domains, and
some folks have created websites where users can enter, one-at-a-time,
domains to check. While providing an easy-to-use interface, this suffers from the
following problems:

* It it tedious to check large numbers of domains
* It requires that you share your browsing information with third-parties that you migh not trust

By contrast, `cloudbleed-browser-scan` allows those comfortable with a
few command-line commands to privately search their web browser's
history for domains that are potentially affected by CloudBleed in a
matter of seconds. This allows you to see if there are any sensitive
domains on the list, and thus you can just change your passwords and
credentials on a hopefully shorter list.

Currently this script will run on Mac OS X, but porting to Linux
should be easy. It currently supports the following browsers:

* Firefox
* Chrome
* Chromium
* Safari
* Tor Browser



More on CloudBleed:
https://en.wikipedia.org/wiki/Cloudbleed

This Git repo has the following essential Git repo as a submodule.
It provides a curated list of potentially-affected sites:
https://github.com/pirate/sites-using-cloudflare



# Install & Use:

Note that this Git repo has the `sites-using-cloudflare` repo as a submodule,
so do note the `--recursive` option to `git clone`:

```
git clone --recursive git@github.com:taltman/cloudbleed-browser-scan.git
cd cloudbleed-browser-scan
./cloudbleed-browser-scan
```

The script prints some helpful messages to STDERR while the script is running.
You can redirect the list of affected domains from STDOUT.


# Feedback

Please feel free to file issues, and to fork & send me pull requests. Thanks!
