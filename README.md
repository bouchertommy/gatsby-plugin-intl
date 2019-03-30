# gatsby-plugin-intl

Internationalize your Gatsby site.

## Features

- Out of box internationalization-framework powered by [react-intl](https://github.com/yahoo/react-intl). 

- Support automatic redirection based on the user's preferred language in browser provided by [browser-lang](https://github.com/wiziple/browser-lang).

- Support multi-language url routes in a single page component. This means you don't have to create separate pages such as `pages/en/index.js` or `pages/ko/index.js`.

## Inspiration

When you build multilingual sites, Google recommends using different URLs for each language version of a page rather than using cookies or browser settings to adjust the content language on the page. [(read more)](https://support.google.com/webmasters/answer/182192?hl=en&ref_topic=2370587)

## Starters

Demo: [http://gatsby-starter-default-intl.netlify.com](http://gatsby-starter-default-intl.netlify.com)

Source: [https://github.com/wiziple/gatsby-starter-default-intl](https://github.com/wiziple/gatsby-starter-default-intl)

## How to use

### Install package

`npm install --save gatsby-plugin-intl`

### Add a plugin to your gatsby-config.js

```javascript
// In your gatsby-config.js
plugins: [
  {
    resolve: `gatsby-plugin-intl`,
    options: {
      // language JSON resource path
      path: `${__dirname}/src/intl`,
      // supported language
      languages: [`en`, `ko`, `de`],
      // language file path
      defaultLanguage: `ko`,
      // option to redirect to `/ko` when connecting `/`
      redirect: true,
    },
  },
]
```

### You'll also need to add language JSON resources to the project.

For example,
language resource file | language
-- | --
[src/intl/en.json](https://github.com/wiziple/gatsby-starter-default-intl/blob/master/src/intl/en.json) | English
[src/intl/ko.json](https://github.com/wiziple/gatsby-starter-default-intl/blob/master/src/intl/ko.json) | Korean
[src/intl/de.json](https://github.com/wiziple/gatsby-starter-default-intl/blob/master/src/intl/de.json) | German

### Change your page component

```jsx
import React from "react"
import { withIntl, Link, FormattedMessage } from "gatsby-plugin-intl"

const IndexPage = ({ intl }) => {
  return (
    <Layout>
      <SEO
        title={intl.formatMessage({ id: "title" })}
      />
      <Link to="/page-2/">
        {intl.formatMessage({ id: "go_page2" })}
        {/* OR <FormattedMessage id="go_page2" /> */}
      </Link>
    </Layout>
  )
}
export default withIntl(IndexPage)
```

## How It Works


Let's say you have two pages (`index.js` and `page-2.js`) in your `pages` directory. The plugin will create static pages for every language.

file | English | Korean | German | Default*
-- | -- | -- | -- | -- 
src/pages/index.js | /**en** | /**ko** | /**de** | /
src/pages/page-2.js | /**en**/page-2 | /**ko**/page-2 | /**de**/page-2 | /page-2

_* If redirect option is `true`, `/` or `/page-2` will be redirected to the user's preferred language router. e.g) `/ko` or `/ko/page-2`. Otherwise, the pages will render `defaultLangugage` language._

## Components

To make it easy to handle i18n with multi-language url routes, the plugin provides several components.

To use it, simply import it from `gatsby-plugin-intl`.

Component | Description
-- | --
withIntl | A higher-order component for pages.
Link | This is a wrapper around @gatsby’s Link component that adds useful enhancements for multi-language routes. All props are passed through to @gatsby’s Link component.
IntlContextConsumer | A context component to get plugin configuration on the component level.
injectIntl | https://github.com/yahoo/react-intl/wiki/API#injection-api
FormattedMessage | https://github.com/yahoo/react-intl/wiki/Components#string-formatting-components
...and more | https://github.com/yahoo/react-intl/wiki/Components


## License

MIT &copy; [Daewoong Moon](https://github.com/wiziple)