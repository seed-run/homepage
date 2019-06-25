# SEED Homepage

[![Netlify Status](https://api.netlify.com/api/v1/badges/446816a0-b43c-45a5-8531-a36ade5840b1/deploy-status)](https://app.netlify.com/sites/seed/deploys)

### Local Usage

To use this repo locally, start by running.

``` bash
$ bundle install
```

And then start the dev server.

``` bash
$ bundle exec jekyll serve
```

You can now view the page at http://localhost:4000

To run it on a different port run:

``` bash
$ bundle exec jekyll serve --port 4001
```

You can also turn on live reloading and incremental builds while editing.

``` bash
$ bundle exec jekyll serve --incremental --livereload
```

### Build

The build script is in `netlify.toml` and it runs the following:

``` sh
./pre-build && jekyll build
```

Where `pre-build` is a script to convert SVGs in the `assets/blog/` dir to PNGs.

### Deploy

To deploy `git push` to `master` branch.

Deploy status can be viewed on the Netlify dashboard.

https://app.netlify.com/sites/seed

To use `jekyll.environment` in template, set `JEKYLL_ENV` to `production` as environment variable in the Netlify dashboard.

### Older Versions

- [Version 1](https://version1--seed.netlify.com/)
- [Version 2](https://version2--seed.netlify.com/)
- [Version 2.1](https://version2-1--seed.netlify.com/)
- [Version 3](https://version3--seed.netlify.com/)
- [Version 3.1](https://version3-1--seed.netlify.com)
- [Version 3.2](https://version3-2--seed.netlify.com)
- [Version 3.3](https://version3-3--seed.netlify.com)
- [Version 3.4](https://version3-4--seed.netlify.com)
