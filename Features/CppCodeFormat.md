# Feature: C++ code formatting

  - **Goal**: Minimize patch conflicts, reduce commit noise, and improve
    code readability.

  - **Status**: completed

  - **Version**: Squid 3.1

  - **Developer**: Christos Tsantilas,
    [AmosJeffries](https://wiki.squid-cache.org/action/show/Features/CppCodeFormat/AmosJeffries#)

## Details

Squid-2 code has a specific format which is enforced on CVS commit.

This project adds a similar format to Squid-3 code. Starting with 3.1.
To format the source correctly you require **astyle version 1.23** and
an **md5sum** (binary or script equivalent).

### When to format.

  - ![(\!)](https://wiki.squid-cache.org/wiki/squidtheme/img/idea.png)
    If you don't have the astyle 1.23 and md5sum tools to do a format
    correctly. Particularly the right version of astyle. We would rather
    you didn't do a format yourself. The formatter script will check and
    omit the format step if you do not have the right version.

Poorly formatted code is often difficult to read so if you do have the
right tools, consider formating before sending a \[PATCH\] or \[MERGE\]
request to squid-dev for auditing (or before committing accepted code).
A global reformat is repeated regularly on trunk, but it saves everybody
trouble and keeps bundlebuggy happy if patches have the right format to
start with.

On the other hand, if you just delete the condition of a large
if-statement or loop and then reformat, it becomes very difficult for
some of the reviewers (and, later, bug chasing developers) to see that
you did not change anything else (or changed something correctly) inside
that former if-statement or loop. Your patch will also be more likely to
cause conflicts with other pending patches.

Make the decision based on tools availability and the formatting impact
on the overall clarity/compatibility of your changes.

### Doing a Reformat

Given the right tools to use. The **scripts/source-maintenance.sh**
script can be run over a checkout of the Squid-3 code to format it
correctly.

This tool does other code checks and rebuilds several compiler system
files as it goes so should always be run from the sources top directory.

### Handling Errors

It will abort on first syntax change leaving a file fubar.h.astylebad
(bad reformat). So a manual diff like so:

    diff -wu fubar.h fubar.h.astylebad

is needed to check whether the reformat worked.

Sometimes code comments get re-arranged. These are picked up as errors
and can be ignored. Simply accept the change by moving the
fubar.h.astylebad into place over the unformatted one and run the
formatter again. It will continue past and locate the next problem.

## astyle

  - [](http://astyle.sourceforge.net/)

[CategoryFeature](https://wiki.squid-cache.org/action/show/Features/CppCodeFormat/CategoryFeature#)
