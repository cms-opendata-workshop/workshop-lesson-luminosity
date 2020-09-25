---
title: "Calculating luminosity"
teaching: 10
exercises: 0
questions:
- "How do I calculate luminosity?"
objectives:
- "Know how to calculate luminosity"
keypoints:
- "One can calculate luminosity offline using the `brilcalc` tool"
---
> ## Helpline
>
> Remember that we are always available to help.  Our [Mattermost][mattermost] channel is open.
{: .callout}

> **NOTE:**
> It is important that you use the `-c web` option when running `brilcalc`.
> This specifies that you use indirect access to BRIL servers via web cache.
> For users of CMS open data outside CERN and CMS this is the only option that will work.
{: .testimonial}

> **NOTE:**
> There is a useful help option for `brilcalc` and its commands:
> ~~~
> brilcalc --help
> ~~~
> {: .bash}
> ~~~
> usage:
>    brilcalc (-h|--help|--version)
>    brilcalc [--debug|--warn] <command> [<args>...]
>
> commands:
>   lumi Luminosity
>   beam Beam
>   trg Trigger configurations
> See 'brilcalc <command> --help' for more information on a specific command.
> ~~~
> {: .output}
{: .testimonial}

{% include links.md %}
