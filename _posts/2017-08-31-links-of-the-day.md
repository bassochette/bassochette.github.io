---
layout: post
title: "links of the day"
category: "links"
date: 2017-08-31 09:29:50
tags:
- links
- symfony
- doctrine2
- twig
---

- [Count with symfony and doctrine](http://sf2.memosdedev.com/faire-un-count-avec-doctrine2-dans-symfony2.html)

- [Twig extensions - internationalization](http://twig-extensions.readthedocs.io/en/latest/intl.html)

Add in `app/config/services.yml`

```yml
twig.extension.intl:
  class: Twig_Extensions_Extension_Intl
    tags:
      - { name: twig.extension }
```
