# The ZMS website

This repo houses the assets used to build the ZMS website, available at http://zmsforextours.com.

## Tools

The website is built and developed using the Static HTML/CSS/JS

## Website content

The content for the [ZMS Website](http://zmsforextours.com) is in [`content/home`](./content/home), while the content for the ZMS documentation is in the [`docs`](./docs) folder.

The latest (edge) version of the documentation lives in the [`docs`](./docs) folder on the `main` branch, and is always viewable on http://zmsforextours.com/docs. Documentation for specific released versions lives in its own release branch, for example `release-2.1.0`.

### Creating a PR

In general, all PRs should be made against the `master` branch to update the edge version of the docs. If you are making a change that also affects released versions, indicate which release branches to update in your PR so the website maintainers can backport your changes.

If you are making a change that is specific to a single released version of documentation, make a PR against that branch (`release-X`). For example, if you are fixing something specific to v2.1.0 you should make a PR against the release-2.1.0 branch only. If you are fixing something that impacts v2.1.0 docs and all future versions, you should make the PR against the `master` branch and so the change can also be backported to the v2.1.0 docs.

A preview of your changes is viewable through the Netlify preview linked in the PR tests. Use this to verify that your changes look good before asking the maintainers for a review. When updating the edge version make sure you add `/docs/edge/` to the preview URL to see your changes.

### Creating release docs

When creating docs for a new release, please create a branch with the format `release-X.Y.Z`.
When you want to make these docs available through the dropdown menu, put the following into the `config.toml` file, above all other versions (versions are linked based on order in the config file):

```
[[params.versions]]
zmsversion = "X.Y.Z"
helmversion = "X.Y"
branchname = "release-X.Y.Z"
``` 

### CSS

The CSS for the site is built from [Sass](https://sass-lang.com) inputs in the [`assets/sass`](./assets/sass) directory. There is also a small amount of JavaScript logic for the site in [`assets/js/app.js`](./assets/js/app.js).

## Publishing the website

The ZMS website is published automatically on the [Domain](http://zmsforextours.com) platform. Whenever changes are pushed to the `main` branch, the site is re-built and re-deployed, usually within about one minute.

## Run the ZMS website locally

### Step 1: Clone project

```sh
git clone https://github.com/zuhairabs/zms.git
cd website
```

## Step 2: Load documentation content

The Markdown content for the Harbor [docs](http://zmsforextours.com/docs) is drawn from the [`docs`](./docs) folder and the `release-X` branches. To pull that content into your local website repo:

```sh
make prepare
```

This copies the `docs` directory and the `release-X` branches into this repo's [`content`](./content) folder, separated by versions, where it can be processed by Hugo.

## Step 3: Install npm dependencies

```sh
npm i
```

## Step 4: Run ZMS in server mode

```sh
make serve
```

This starts up the local Hugo server on http://localhost:1313. As you make changes, the site refreshes automatically in your browser.

## Checking links

To run the link checker for the Harbor website:

```sh
make check-internal-links
```

This command builds the site (including drafts and future content), downloads the [htmltest](https://github.com/wjdp/htmltest) link checker into your local directory, and runs the checker in accordance with the configuration specified in [`.htmltest.yml`](./.htmltest.yml). Only internal links are checked and all errors are piped to stdout.
