# RandomDSdevel's Thoughts on an Ideal Personal Package-Management Workflow

## Introduction

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;I've used [Homebrew](https://github.com/Homebrew/brew) as my system package manager since August 22<sup>nd</sup>, 2014, but have become increasingly dis-satisfied with it over the past few years.  Homebrew has changed from being a 'from-source' package manager vending packages suitable for arbitrary user configuration to being a binary package manager distributing packages with limited end-user configurability.  I therefore thought I'd put some personal musings on what I might consider an ideal package-management workflow and what would enable it down for future reference.  (Note, however, that I do not personally have the resources to expand further upon this at the present time.)  

## Minimal Guiding Principles

- Upstream's source code is always the ultimate source of truth.  
- End-user package configurability must remain maximized.  
- A package manager's community's members should do their utmost to ensure that they maintain robust support for each other's use cases.  

## Ideas

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;If I were to construct a package manager and package-management ecosystem and workflow from scratch, here's what I'd take inspiration from:  

- [Homebrew](https://github.com/Homebrew/brew):  
  - I've generally always been happy with most, if not all, of Homebrew's command repertoire and the general logic behind the project's interface except for a few bits and pieces here and there, though there are some things about it that I'd prefer were different and would change:  
    - '`reinstall`' should accept build-recipe options, using them to add to, remove from, and otherwise manipulate how one wants to reinstall packages.  Homebrew currently disfavors/disallows this.  
    - Some commands should produce more output for informational purposes, at least when asked to.  Some examples of where I find Homebrew lacking in this department today are:  

      - '`brew update`:'  

        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;In order to see the full SHA-256 checksums of the repositories affected by this command before and after it modifies them by syncing your local copies of them with upstream, one currently has to enable verbose (and probably also debugging) output.  There should be an independent option to enable reporting for more of the underlying version-control operations involved here, separate from '`--verbose`' and '`--debug`.'  

      - Generally:  
        - More reporting should be presented to the user with respect to which operations consult or modify the package manager's backing package repository.  

    - All functionality related to any sort of binary package distribution, such as the 'bottling' functionality provided by Homebrew, should be a separate project, if it exists at all.  
  - What I'd keep:  
    - As stated above, most of the interface and command repertoire.  
    - The fact that Homebrew requires any patches needed to make packages build be submitted and accepted upstream for inclusion in an upcoming version of the software which failed to build and install prior to using them against the version of that/those package(s) initially found to be broken.  
    - The philosophy of primarily building from and distributing the most recent stable release at all times even if other, older, discouraged versions alternatively remain available for a time for any reason.  (Cases in which older versionss' availability might be acceptable include:  
      - The one in which an older version's availability would be acceptable is if another package depends on said older version of the former package and can't yet migrate to a newer one.  
      - if migrating data between two versions of a package isn't straightforward or is even difficult or error-prone.  
      - Other motivations for this exist, but I won't list them here, at least not yet.)  
- [The Debian package-management system](https://wiki.debian.org/DebianPackageManagement) (APT, '`apt-get`,' etc.,) from what I've heard of it:  
    - Its preference toward forbidding vendoring of dependencies.  If a package has an external dependency, it should use a(n) instance/copy of it provided by the package manager if at all possible.  
- [Gentoo](https://www.gentoo.org/) ([About](https://www.gentoo.org/get-started/about/), [Wiki](https://wiki.gentoo.org/wiki/Main_Page)) and [Gentoo Prefix](https://wiki.gentoo.org/wiki/Project:Prefix):  
  - Configuration choice for users.  
  - All packages are built from source on end-users' machines by default.  (The provision of any pre-built binary packages could be handled by another project built on top of a package manager fitting the criteria supplied within this document, but should always be kept separate per point two of [the Unix philosophy](https://en.wikipedia.org/wiki/Unix_philosophy#Mike_Gancarz:_The_UNIX_Philosophy) on, "Mak[ing] each program do one thing well," and [the principle of separation of concerns](https://en.wikipedia.org/wiki/Separation_of_concerns).)  

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Additionally, I'd heavily prefer that:  

- If upstream provides a configuration option for a package, then the new package manager should have a corresponding build-recipe option to trigger using it, _with few to no exceptions!_  (That's not to say that this would necessarily be the case at first or that they'd all work all the time, though effort should be made to ensure that option breakage is as minimized and limited in temporal scope as possible.)  
- If something's broken or not yet supported or otherwise available, it should error out as early as possible, preferrably with a message provided before any involved build recipes invoke package configuration and build steps.  (Homebrew already does this, to some extent, but it doesn't have this principle codified explicitly.)  
- Integration between any package manager derived from the ideas presented here and programming-language–specific package managers is seamless and completely painless:  users should be able to access programming-language–specific packages as if they were packages native to any package manager meeting the criteria listed in this document.  

## Sources

- [Homebrew's home page](https://brew.sh/ "Home Page For 'Homebrew:  The missing package manager for macOS.'") and content linked form there. 
- The [Gentoo wiki](https://wiki.gentoo.org/wiki/Main_Page)'s [main 'Foundation' page](https://wiki.gentoo.org/wiki/Foundation:Main_Page)

---

Copied from [a comment on the Gist this used to be](http://web.archive.org/web/20190110205134/https://gist.github.com/RandomDSdevel/50d39b326855b454237b14a091a907db#gistcomment-2793793):  

> &nbsp;&nbsp;&nbsp;&nbsp;Some additional notes:  
>
> 1. This is likely and obviously incomplete.  
> 1. I can't personally pursue any sort of project which this document might imply at the moment.  
> 1. If anybody wants to pilfer any of the ideas listed here for future improvements to an existing package manager, a novel package manager, or a fork of an existing package manager, feel free to go ahead and do just that.  
> 1. I may eventually move this into [my 'RandomDSdevel Evolution' repository](https://github.com/RandomDSdevel/RandomDSdevel-Evolution) or reference whatever other repository this document ends up in there by including it as a Git submodule.  
>
> ⋮

(Editor's Note:  Moved, but not yet referenced elsewhere.)  

> ⋮
>
> With respect to point 3, CC @chdiza, @zbeekman, @DomT4, @blogabe, and @danieljl because of the nature of their participation in Homebrew/homebrew-core#31510, which is what finally inspired me to type these initial pondering up.  
>
> (Edit:  Added @danieljl to the list of potentially interested GitHub users above.)  
>
> ---
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Also, bonus points go to whoever, me or otherwise, might pick this up in future if they can make migrating to this new solution from at least one existing package manager, namely Homebrew, as painless as possible.  (It would be awesome if somebody could do this for _all_ package managers, but that's…a daunting task to ask of anyone.)  

(Editor's Note:  See also [issue #4](https://github.com/portage-brew/portage-brew/issues/4).)  
