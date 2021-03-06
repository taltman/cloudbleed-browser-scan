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
git clone --recursive https://github.com/taltman/cloudbleed-browser-scan.git
cd cloudbleed-browser-scan
./cloudbleed-browser-scan
```

The script prints some helpful messages to STDERR while the script is running.
You can redirect the list of affected domains from STDOUT. The output
consists of the following fields:

* URL
* Number of times visited (summed across all browsers)
* Date of last visit (most recent across all browsers)

The two additional metadata fields make it very easy to whittle down a
large list. Here's an example session:

```
> time ./cloudbleed-browser-scan > scan.txt
Loading CloudFlare domain list...
Loaded 4287589 domains.
Found 359 CloudFlare-associated domains out of 66235 domains from your
browsers.

> awk -F'\t' '$2 > 10' scan.txt | wc -l
28
```

The above can read as saying that out of the 4,287,589 domains
currently associated with CloudFlare, 359 were also found in my
browsing history of 66,235 domains. Since the bug is reported as
having been introduced in September 2016, the output is restricted by
default to sites visisted afterwards. Furthermore, by eyeballing the
`scan.txt` list, I noticed that sites that I had visited fewer than
ten times were sites that did not contain any important information on
them. Applying these restrictions, I was left with 28 sites to
scrutinize manually. Of these, twelve are sensitive, and I will
definitely change my passwords there.

Definitely a lot easier than entering in 66,235 domains into a
Cloudbleed-checking website tool! :-)


# Feedback

Please feel free to file issues, and to fork & send me pull requests. Thanks!

# Acknowledgements

Thank you to the following people:
* axelsimon for suggesting to remove the dependency on having a GitHub account
