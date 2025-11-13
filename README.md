# [StARLinG Lab](https://starling-lab.github.io)

[![][license img]][license] [![][release img]][release]

## Overview

StARLinG Lab's website hosted on GitHub Pages. Built with Jekyll, jQuery, and the minimal-mistakes Jekyll theme.

Maintained by **[Alexander L. Hayes](https://github.com/batflyer)** and **[Harsha Kokel](https://github.com/harshakokel)**.

Contact: `{alexander.hayes/harsha.kokel}@utdallas.edu`

## Quick-start Guide (Linux and OSX)

* Install Ruby and RubyGems (refer to Jekyll [installation](https://jekyllrb.com/docs/installation/) and [quick-start guide](https://jekyllrb.com/docs/quickstart/)).
* `git clone https://github.com/starling-lab/starling-lab.github.io.git`
* `gem install jekyll bundler`
* `bundle install`
* `bundle exec jekyll serve`
* Navigate to `127.0.0.1:4000` in your browser.

## Publishing the Website

The website is automatically deployed to GitHub Pages when changes are pushed to the main/master branch.

1. Make your changes locally
2. Test with `bundle exec jekyll serve`
3. Commit and push to the repository
4. GitHub Pages will automatically build and deploy the site

The site will be available at: https://starling-lab.github.io

## Updates guide

1. Publications are in `/_data/publication.yml`
2. News updates go in `/_news/...`
3. Lab member details are in `/_data/authors.yml`
4. Gallery photos are in `/_pages/photo-gallery.md`
5. Top navigation is in `/_data/_navigation.yml`

## Contributing

Refer to [CONTRIBUTING.md](.github/CONTRIBUTING.md) for documentation on submitting issues and pull requests.

A [Guide to Updating the Website](.github/docs/README.md) has more information on how to author new pages, and the same directory has templates that may be useful.

## License

This work is licensed under a [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/). See [LICENSE.txt](LICENSE.txt) for a full copy of the license.

## Attribution

This work incorporates work from the following sources:

* ["Minimal Mistakes"](https://github.com/mmistakes/minimal-mistakes/) a Jekyll theme by Michael Rose and contributors, distributed under the terms of the [MIT License](https://github.com/mmistakes/minimal-mistakes/blob/master/LICENSE.txt).
* ["jekyll"](https://jekyllrb.com) a blog-aware, static site generator in Ruby, distributed under the terms of the [MIT License](https://github.com/jekyll/jekyll/blob/master/LICENSE).
* ["linkprediction.jpg"](https://raw.githubusercontent.com/starling-lab/starling.utdallas.edu/v1.0-master/assets/images/linkprediction.jpg) is plotted and rendered with [Cytoscape](http://www.cytoscape.org/download.php), used under the terms of the LGPL.
* The random student loading on the homepage is based on a blog post by [James W Thorne](https://thornelabs.net/2014/06/08/a-better-way-to-display-random-jekyll-posts-on-page-load-or-refresh-using-jquery-and-json.html).
* The StARLinG Logo is designed by [Gautam Kunapuli](https://www.utdallas.edu/~Gautam.Kunapuli/), and used with permission.

[license]:LICENSE.txt
[license img]:https://img.shields.io/github/license/starling-lab/starling-lab.github.io.svg

[release]:https://github.com/starling-lab/starling-lab.github.io/releases
[release img]:https://img.shields.io/github/tag/starling-lab/starling-lab.github.io.svg
