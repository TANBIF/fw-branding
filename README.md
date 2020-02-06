## Introduction

This is a base branding for new Living Atlas deployments. That is, some ALA header, banner and footer theme with:

- Well integration with ALA modules trying to avoid jquery conflicts and similar
- Well integration with `CAS` Authentication
- Multilingual
- Modern javascript code without lost compatibility with old browsers

You can use this as a basis for a new LA infrastructure branding or just to see how you can integrate your branding with ALA dependencies, etc.

## Styling

ALA uses Bootstrap version 3 in most of their modules.

Additionally we use:
- Material Design Lite https://getmdl.io/ with a custom theme that you can https://getmdl.io/customize/index.html change, download and put instead of `app/css/material.min.css`.
Anyway you can drop any of these last dependencies and create your header/footer from scratch with your own style. See `app/assets/head*.html` for more details.
- And experimentally also [Material Bootstrap Design](https://github.com/FezVrasta/bootstrap-material-design) to have similar style in the ALA modules.
If you only want to do minor style changes, have a look to `app/css/material-custom-styles.css`.

This styling is not the most important work of this branding, but instead the integration with ALA and the brunch configuration that gives you the possibility to use modern javascript code and modern libraries or use `i18next`, for example.

## Structure

```
├──app
│   ├── assets           # static assets, like index/header/footer/banner.html
│   │   ├── fonts        # etc
│   │   ├── locales
│   │   └── images
│   ├── css              # put your css here
│   ├── (...)
│   └── js               # put your js code here
│
├──commonui-bs3-2019     # ALA branding as submodule
│
├──node-modules          # 'yarn add module', to install
│                        # any node module and use it in your js code
└──public
    ├── css              # The 'public' directory is what you have to deploy
    │   └── images       # It's generated by `brunch`
    ├── fonts
    ├── locales
    ├── images
    └── js
```
Brunch compiles in public your `js`/`css` and make this compatible with older browsers (so you can use node modules or ES6 code without problems).

## Basic settings

See and edit `app/js/settings.js`.

## Development

This is using https://brunch.io instead of gulp and using [ALA commonui-bs3-2019](https://github.com/AtlasOfLivingAustralia/commonui-bs3-2019) as a git submodule to use the same assets used by ALA modules.

### Usage

```
# First use
yarn install

# During development
brunch watch
# or
brunch build
# or
brunch build --production
```

Test with:
- http://localhost:3333/
- http://localhost:3333/testPage.html

## Deployment and ALA configuration

```
brunch build --production
rsync -a --delete public/ l-a.site:/srv/l-a.site/www/test-skin/
```

And in your inventories:

```
header_and_footer_baseurl = https://l-a.site/test-skin
header_and_footer_version = 2
```

The `version = 2` will substitute some `::variables::` like login/logout urls in your `head/banner/footer.html` in production. This is also done in `index.html` and during development with the `app/js/settings.js` values. See [ala-bootstrap3 HeaderFotterTagLib.groovy ](https://github.com/AtlasOfLivingAustralia/ala-bootstrap3/blob/351067716c685dc9a896d0a57abd1b4afdfaee39/grails-app/taglib/au/org/ala/bootstrap3/HeaderFooterTagLib.groovy#L218) for more details. Use the appropriate skin (see below).

### About skin.layouts recommend to use on each ALA modules

In general you should use `main` skin in your ALA modules, except for:
- `collectory`: use `ala` skin

## Why brunch?

We can use node modules, ES6 js code, sourcemaps, minimize, development with watch and browser auto reload etc, all this without suffering with gulp configuration.

We copy the ALA dependencies (jquery, autocomplete, etc)  so we can integrate ALA modules well.

See the `brunch-config.js` for more details.

## TODO

- [ ] use of SASS and better style customization options
- [ ] Integration of some EU cookie utility like: https://www.npmjs.com/package/@beyonk/gdpr-cookie-consent-banner
- [ ] LA occurrences, etc stats in index

PR welcome!

## License

Apache-2.0 © 2020 [Living Atlases](https://living-atlases.gbif.org)

Additionally:

- Some `html`/`css`/`js` based in Material Design Lite, Apache License 2.0.
- Bootstrap Material Design, MIT license.

## More information

- https://github.com/AtlasOfLivingAustralia/documentation/wiki/Styling-the-web-app