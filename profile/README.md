## Description

This organization contains the repos used to publish content for https://wikip.co/

## Instructions

These instructions illustrate the purpose of each repo.

### Pubic Repo

URL: https://github.com/wikip-co/public

The public repo contains the final product of all the static assets that are published to the web.  Publishing is provided by Cloudflare Pages (https://pages.cloudflare.com/).  This repo is linked to a Cloudflare Pages account, and each time a change is detected, it kicks off a new build.  No building is required in this particular instance, since we are pushing static html to the repo.

To get this static html, this public repo is added as a submodule in each of the other repos.  The other repos contain the tools necessary to build and process content.  They each represent either the root or different sub-directory sites that write files to specific folders in the public repo.

### Main Source Repo

URL: https://github.com/wikip-co/main_source

The main source repo is used to publish a single-page website to the root of https://wikip.co/.  The purpose of this root page is to list the links to all the active sub-directories being published.  Each of these sub-directories is a self-contained, multi-page site with its own distinct css and resource files.

### Sample sub-directory site repo

URL: https://github.com/wikip-co/modern-history_source

The url above is an example of a repo that is used to publish content for the subdirectory https://wikip.co/modern-history/.

When updates are made to this repo, the generated html files are pushed to the public repo (https://github.com/wikip-co/public) under the modern-history/ folder.  This is done by adding the public repo as a submodule and editing the site config accordingly.

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
Edit the following portion of the _config.yml, replacing the <variables> accordingly:
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
Example package.json
```
{
  "name": "hexo-site",
  "version": "0.0.0",
  "private": true,
  "scripts": {
    "build": "./node_modules/hexo/bin/hexo generate",
    "clean": "hexo clean",
    "deploy": "hexo deploy",
    "server": "./node_modules/hexo/bin/hexo server"
  },
  "hexo": {
    "version": "6.3.0"
  },
  "dependencies": {
    "hexo": "^6.0.0",
    "hexo-directory-category": "^1.1.4",
    "hexo-generator-category": "^1.0.0",
    "hexo-generator-index": "^2.0.0",
    "hexo-generator-search": "^2.4.3",
    "hexo-generator-tag": "^1.0.0",
    "hexo-renderer-ejs": "^2.0.0",
    "hexo-renderer-markdown-it": "^5.0.0",
    "hexo-renderer-stylus": "^2.0.0",
    "hexo-server": "^3.0.0"
  }
}
```
These sites are built using npm and hexo-cli.  If you have nodejs installed, you can simply run the following commands to build and test the site:
```
$ npm install
$ hexo s # starts the web server
$ hexo generate # generates the static files at public/<site-name>/
```
