---
title: Bluemix CloudFoundry Deployment
layout: en
permalink: /user/deployment/bluemixcloudfoundry/
---

You now have the ability to deploy directly to [IBM Bluemix](https://console.ng.bluemix.net/) after a successful build on Travis CI.

## Getting on the Edge

Proper Bluemix CloudFoundry support is currently included only in the edge version of Travis.  See how to enable it via the `.travis.yml` below.

## The Easy Way

Go grab [the Travis gem from GitHub](https://github.com/travis-ci/travis.rb) and run this command:

```sh
travis setup bluemixcloudfoundry
```

You will need the following information about your Bluemix environment: username, password, organization, space, and region. Available Bluemix regions are US South (ng) London (eu-gb), and Sydney (au-syd). Travis offers to encrypt your passwod, and will take care of the rest. Learn more about [managing organizations and spaces](https://console.ng.bluemix.net/docs/admin/orgs_spaces.html).

## The Slightly Harder Way

You can also directly edit your `.travis.yml`. Insert the following to get up and running:

```yaml
 deploy:
   edge: true
   provider: bluemixcloudfoundry
   username: brian_knobbs@example.com
   password: somewhatsecretpassword
   organization: myawesomeorganization
   space: staging
   manifest: manifest-prod.yml          # (optional)  Defaults to manifest.yml.
   region: eu-gb                        # (optional)  [ng, eu-gb , au-syd] Defaults to US South region (ng).
   api: https://api.ng.bluemix.net      # (optional)  Overrides region setting if specifed for Bluemix local installations.
```

***Make sure that you encrypt your password before pushing your updated .travis.yml to GitHub.***

You can do this using the Travis gem by running:

```sh
travis encrypt --add deploy.password
```

If your password includes symbols (such as braces, parentheses, backslashes, and pipe symbols), [you must escape those symbols before running `travis encrypt`](/user/encryption-keys/#Note-on-escaping-certain-symbols).

### Conditional releases

You can deploy only when certain conditions are met.
See [Conditional Releases with `on:`](/user/deployment#Conditional-Releases-with-on%3A).
