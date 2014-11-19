drupal-globalredirect
=====================

What?

GlobalRedirect is a simple module which…

    Checks the current URL for an alias and does a 301 redirect to it if it is not being used.
    Checks the current URL for a trailing slash, removes it if present and repeats check 1 with the new request.
    Checks if the current URL is the same as the site_frontpage and redirects to the frontpage if there is a match.
    Checks if the Clean URLs feature is enabled and then checks the current URL is being accessed using the clean method rather than the 'unclean' method.
    Checks access to the URL. If the user does not have access to the path, then no redirects are done. This helps avoid exposing private aliased node's.
    Make sure the case of the URL being accessed is the same as the one set by the author/administrator. For example, if you set the alias "articles/cake-making" to node/123, then the user can access the alias with any combination of case.
    Most of the above options are configurable in the settings page. In Drupal 5 you can access this after enabling the globalredirect_admin module. In Drupal 6, the settings page is bundled into the module.

Why?

Once enabled, an alias provides a nice clean URL for a path on a site. However Drupal does not remove the old path (eg node/1234). The problem is that you now have two URLs representing the same content. This is dangerous territory for duplicate pages which can get you sandboxed by the search engines!
How?

This module uses hook_init to interrupt the page load and action the alias lookups. If any of the above rules apply then the appropriate action is taken. If no rules apply then the page load continues uninterrupted. An example of this in use is on the site it was developed for. http://www.sportbusiness.com/node/160559 will redirect to http://www.sportbusiness.com/news/160559/lagardere-sets-up-sports-division due to the alias setup on this site.
Anything I Should Know?

As with most modules - there are often a few things you should be aware of before going ahead.

    I recommend using the 6.x-1.5 or 7.x-1.5 release, depending on your Drupal install version.
    It is important to know that if your site is in maintenance mode then Global Redirect does not function. This is intentional behaviour.
    Known Bugs:
        The 7.x-1.4 release has known issues with multilingual sites. See #1378690: Update to 7.x-1.4 adds duplicate language prefixes, causing a redirection loop. This is fixed in 7.x-1.5.
        Issues with Windows IIS Server. There is a known issue with Clean URL's in IIS and there is also a known issue with certain versions of PHP running on IIS where a Permanent Redirect (301) is incorrectly sent as Object Moved (302).
        Multilingual sites should thoroughly check their site after enabling this module. There have previously been known issues with i18n causing redirect-loops and such. I believe these have been fixed, but please take care.
        Drupal For Facebook. The main problem with this is similar to i18n. Both modules use Custom URL Rewriting which appears to confuse GlobalRedirect.

