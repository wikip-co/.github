## Description

This organization contains the repos used to publish content for https://wikip.co/

## Instructions

These instructions illustrate the purpose of each repo and how files get published to the web.

### Pubic Repo

URL: https://github.com/wikip-co/public

The public repo contains the final product of all the static assets that are published to the web. This public repo is added as a submodule in each of the other repos.  The other repos represent different sub-sites that write files to specific subfolders in the public repo.

### Main Source Repo

URL: https://github.com/wikip-co/main_source

The main source repo is used to publish a single-page website at the root of http://wikip.co.  The purpose of this page is to list links that point to active sub-directories being published.  Each of these sub-directories is a self-contained, multi-page site with its own distinct css and source files.

### Sample sub-directory repo

URL: https://github.com/wikip-co/modern-history_source

The url above is an example of a repo that is used to publish content for https://wikip.co/modern-history/

When updates are made to this repo, the generated static html files are pushed to the public repo (https://github.com/wikip-co/public).  This is done by adding the public repo as a submodule.

#### Example creating a new repo

When creating a new repo for a new sub-directory follow these steps. 

Add the following files:
```
source/_data/description.yml
source/_data/resources.yml
source/_posts/post.md
.gitignore
_config.yml
package.json
```
Add the following submodules:
```
git submodule add git@github.com:wikip-co/public.git public/`
git submodule add git@github.com:wikip-co/wiki_theme themes/`
```
Verify submodules are added:
```
$ git submodule init
$ git submodule update
```
Edit the following portion of the _config.yml, replace <variables> accordingly:
```
title: <Site Name>
subtitle: 'Documentation'
description: 'Research'
keywords:
author: <Author>
language: en
timezone: ''
url: https://wikip.co/<site-name>
root: /<site-name>/
permalink: :post_title/
permalink_defaults:
pretty_urls:
  trailing_index: true
  trailing_html: true
source_dir: source
public_dir: public/<site-name>
```
Sample resources.yml
```
title: <Site Name>
cloudinary_user: <Cloudinary Username>
image_transform: /image/upload/w_200,f_auto/
image_cloud: https://res.cloudinary.com/
favicon:
```
