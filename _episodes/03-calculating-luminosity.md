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
> Of particular use will be the `brilcalc lumi` command.
{: .testimonial}

> ## Calculating luminosity for a particular run
> Let's calculate the integrated luminosity for a particular run found in the CMS Open Data.
>> brilcalc lumi -c web -r 160431
> {: .bash}
> ~~~
> #Data tag : 19v3 , Norm tag: onlineresult
> +-------------+-------------------+-----+------+----------------+----------------+
> | run:fill    | time              | nls | ncms | delivered(/ub) | recorded(/ub)  |
> +-------------+-------------------+-----+------+----------------+----------------+
> | 160431:1615 | 03/14/11 03:08:07 | 243 | 218  | 8781.334977241 | 7879.289611261 |
> +-------------+-------------------+-----+------+----------------+----------------+
> #Summary:
> +-------+------+-----+------+-------------------+------------------+
> | nfill | nrun | nls | ncms | totdelivered(/ub) | totrecorded(/ub) |
> +-------+------+-----+------+-------------------+------------------+
> | 1     | 1    | 243 | 218  | 8781.334977241    | 7879.289611261   |
> +-------+------+-----+------+-------------------+------------------+
> ~~~
> {: .output}
{: .challenge}

> ## Luminosity and certified data
> During data talking only those runs in which all the subdetectors, triggers, luminosity, and physics objets are found to be performing as expected
> are certified as "good for physics". For the physics analyst the list of certified luminosity sections in these runs is provided in the form of a
> JSON file. To ensure that we are calculating the luminosity for certified data one must fetch these files and pass them to `brilcalc` on the command > line.
> First let's fetch the JSON file for 2011 data:
> ~~~
> wget http://opendata.cern.ch/record/1001/files/Cert_160404-180252_7TeV_ReRecoNov08_Collisions11_JSON.txt
> ~~~
> {: .bash}
> Then pass this file to `brilcalc` on the command line and pipe it to a text file `2011lumi.txt`:
> ~~~
> brilcalc lumi -c web -i Cert_160404-180252_7TeV_ReRecoNov08_Collisions11_JSON.txt > 2011lumi.txt
> ~~~
> {: .bash}
> The beginning of the output in the file should look like this:
> ~~~
> #Data tag : v1 , Norm tag: onlineresult
> +-------------+-------------------+------+------+----------------+---------------+
> | run:fill    | time              | nls  | ncms | delivered(/ub) | recorded(/ub) |
> +-------------+-------------------+------+------+----------------+---------------+
> | 160431:1615 | 03/14/11 03:14:43 | 200  | 200  | 7366.884       | 7366.875      |
> | 160577:1622 | 03/16/11 01:44:38 | 53   | 53   | 1719.888       | 1631.386      |
> | 160578:1622 | 03/16/11 02:20:03 | 175  | 175  | 5201.105       | 4952.155      |
> | 160871:1636 | 03/19/11 02:43:57 | 141  | 141  | 109739.586     | 106354.581    |
> | 160872:1636 | 03/19/11 03:50:05 | 38   | 38   | 28346.738      | 23977.109     |
> | 160873:1636 | 03/19/11 04:20:20 | 147  | 147  | 104914.534     | 103031.004    |
> ~~~
> {: .output}
> With a summary at the end of the file:
> ~~~
> #Summary:
> +-------+------+--------+--------+-------------------+------------------+
> | nfill | nrun | nls    | ncms   | totdelivered(/ub) | totrecorded(/ub) |
> +-------+------+--------+--------+-------------------+------------------+
> | 194   | 470  | 159872 | 159872 | 5253793895.474    | 5100199528.945   |
> +-------+------+--------+--------+-------------------+------------------+
> ~~~
> {: .output}
{: .challenge}

> ## Luminosity over a range of runs
> Using the `brilcalc lumi --help` and the information found  from [this page](http://opendata-dev.web.cern.ch/record/1001) on the CERN Open Data Portal, how does one calculate the
> integrated luminosity for certified lumi sections for RunA of the 2011 data release?
>> ## Solution
>> RunA of 2011 proton-proton data comprises runs 160431 to 173692 (inclusive) so to calculate the integrated luminosity for this era run the command (where we pipe the output to a text file):
>>> brilcalc lumi -c web --begin 160431 --end 173692 -i Cert_160404-180252_7TeV_ReRecoNov08_Collisions11_JSON.txt > RunA2011lumi.txt
>> {: .bash}
> {: .solution}
{: .challenge}

> ## Select luminometer
>
{: .challenge}

> ## Integrated luminosity for a HLT trigger path
>
{: .challenge}

{% include links.md %}
