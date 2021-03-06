# addons-dev

Addons Forge

## Typical development workflow:

* [Fork](#fork) - once per person
* [Clone](#clone) - once per computer
* [Create new branch](#create-new-branch) - once per addon (or set of addons). For managers only, because push access is needed.
* [Get branch from upstream](#get-branch-from-upstream) - once per addon
* [PR to addons-dev](#pr-to-addons-dev) - as much as needed.
* [Merge PR to addons-dev](#merge-pr-to-addons-dev) - as much as needed. For managers only.
* [Final PR to target repo](#final-pr-to-target-repo) - once per addon
* After accepting Final PR, addon is published at [apps store](https://www.odoo.com/apps/modules/browse?order=Newest) automatically with a delay of up to 24 hours
* Further updates - PRs are sent directly to target repo.

# Fork
Click Fork button at top right hand corner

# Clone

* Clone your fork to your machine:

        git clone git@github.com:USERNAME/addons-dev.git

* Add remotes

        cd addons-dev

        git remote add upstream          git@github.com:it-projects-llc/addons-dev.git
        git remote add misc-addons       https://github.com/it-projects-llc/misc-addons.git
        git remote add pos-addons        https://github.com/it-projects-llc/pos-addons.git
        git remote add mail-addons       https://github.com/it-projects-llc/mail-addons.git
        git remote add access-addons     https://github.com/it-projects-llc/access-addons.git
        git remote add website-addons    https://github.com/it-projects-llc/website-addons.git
        git remote add l10n-addons       https://github.com/it-projects-llc/l10n-addons.git

# Create new branch

    # specify target, repo and branch:
    export REPO=misc-addons BRANCH=11.0 FEATURE=some_feature

    # fetch remote
    git fetch ${REPO}

    # create new branch
    git checkout -b ${REPO}-${BRANCH}-${FEATURE} ${REPO}/${BRANCH}

    # push to upstream
    git push upstream ${REPO}-${BRANCH}-${FEATURE}
    
    # done

# Get branch from upstream


    # get branch from upstream
    git fetch upstream misc-addons-11.0-some_feature
    git checkout -b misc-addons-11.0-some_feature upstream/misc-addons-11.0-some_feature


# PR to addons-dev

   
    # work and make commits
    git commit ...
   
    # push to origin
    git push origin misc-addons-11.0-some_feature
   
    # create pull request via github interface to it-projects-llc/addons-dev repo

# Merge PR to addons-dev

Usually, ``Squash and merge`` button is used to merge PR. In that case, update PR reference to avoid wrong reference after merging to target repo. For example, suggested comment was

    [ADD] pos product category discount (#178)

One need to update it as following:

    [ADD] pos product category discount (it-projects-llc/addons-dev#178)
    

Otherwise after merging to target repo the link will be 

https://github.com/it-projects-llc/pos-addons/pull/178

instead of 

https://github.com/it-projects-llc/addons-dev/pull/178

# Final PR to target repo

    # example for misc-addons
    cd /path/to/misc-addons

    # add remote if it doesn't exist yet
    git remote add addons-dev https://github.com/it-projects-llc/addons-dev.git

    # fetch remote
    git fetch addons-dev misc-addons-11.0-some_feature

    # create branch
    git checkout -b 11.0-some-feature addons-dev/misc-addons-11.0-some_feature

    # push to your fork of target repo
    git push origin 11.0-some-feature

    # create PR to target repo
