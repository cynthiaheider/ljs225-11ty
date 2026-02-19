## Summary
An experiment in porting over the [EditionCrafter](https://editioncrafter.org/) tool to work in [11ty](https://www.11ty.dev/), inspired by the [Hugo implementation](https://github.com/cu-mkp/editioncrafter-project) created by the [Making and Knowing Project at Columbia University](https://scienceandsociety.columbia.edu/content/research-cluster-making-and-knowing-project) - see my implementation of this at https://github.com/cynthiaheider/ljs225-editioncrafter. The EditionCrafter tool generates an interface to display digital critical editions using a IIIF manifest and HTML files from TEI-encoded XML files.

This project uses pre-existing TEI-encoded XML files and [images downloaded from OPenn](https://openn.library.upenn.edu/Data/0001/html/ljs225.html) from pages 15r-19r of [Litterarum simulationis liber](https://find.library.upenn.edu/catalog/9948179063503681?hld_id=resource_link_0), also known as LJS 225, a work on cryptography in the collections of the Kislak Center for Special Collections at the University of Pennsylvania. 

## Contents
- ```_data``` contains TEI-encoded XML files
- ```_site``` contains the site files that push to the GitHub Pages display of the site at https://cynthiaheider.github.io/ljs225-11ty. It automatically generates when ```npx @11ty/eleventy --serve``` is run (local dev) or in the site build pipeline to GitHub Pages controlled by the GitHub Action. What is generated in this folder upon running 11ty is determined in ```eleventy.config.js``` and ```eleventy.js```.
- ```assets/css``` contains EditionCrafter CSS files that change how certain TEI annotations display in the viewer
- ```images``` contains the JPG images of the manuscript pages downloaded from OPenn
- ```ljs225-combined``` contains the HTML and XML files and a IIIF manifest generated upon running the ```editioncrafter process``` command
- ```node_modules``` contains the necessary software dependencies required to build this site with 11ty
- ```how-to-use.md``` contains my attempt at codifying all the steps that go into making EditionCrafter work and generating the site without server-side errors

## Current issues
The viewer loads in the browser lcoally, and appears to be correctly loading both the "Original" and "Decoded" text layers. For some reason GitHub  Pages does not appear to be deploying. I need to be careful with this project because of its reliance on calls to the cynthiaheider.github.io site, which can result in exceeded rate limit errors.
