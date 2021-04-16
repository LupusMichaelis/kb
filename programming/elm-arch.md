# Objective

* explains how Elm is working
* explains bricks to use
* pointers to documentation and the like
* how it comes together

# Resources

## Documentation

Browse those resources to learn Elm.

We're using Elm *0.18*. It's a young language that is evolving quickly and for which
backward compatibility is far from being a feature. Beware of the resources your using,
try not to use features that have been deprecated in current version. Such an example is
the operator specialisation, which has been removed by Elm architects as they gauge it's
been abused.

Online tools:

- [Online console](http://elm-lang.org/try)
- [Ellie](https://ellie-app.com/new)

FAQ, Howtos and the lilke:

- The [beginner guide](https://elmprogramming.com/) is the place to start, I couldn't
  stress it more: it's the ultimate Elm noob bible. Read that first!
- You should get through the [basic syntax](https://elm-lang.org/docs/syntax) doc, to
  make Elm comfy.
- [Language guide](https://guide.elm-lang.org/).
- [Official Elm architecture tutorial](https://github.com/evancz/elm-architecture-tutorial).
- [Unofficial tutorial](https://www.elm-tutorial.org/en/). It's flawed (like views mixed up within the model),
  but in an overall, it's helping much.
- [Community FAQ](http://faq.elm-community.org/)
- [Package design guidelines](https://package.elm-lang.org/help/design-guidelines#keep-tags-and-record-constructors-secret)

References:

- [ELM GitHub HQ](https://github.com/elm-lang)
- [https://package.elm-lang.org/packages/elm-lang/core/5.1.1/](Core language) reference.
- [https://package.elm-lang.org/packages/elm-lang/html/2.0.0/](HTML package) reference.
- [https://package.elm-lang.org/](Other package) reference.

## Extra helper

* elm-community extras
    - [List.Extra](https://package.elm-lang.org/packages/elm-community/list-extra/latest/)
    - [List.Split](https://package.elm-lang.org/packages/elm-community/list-split/latest/)
    - [Dict.Extra](https://package.elm-lang.org/packages/elm-community/dict-extra/latest/)
      Provides helpers to get element by position, zip, chop'n'slice!
    - [Html.Extra](https://package.elm-lang.org/packages/elm-community/html-extra/latest/)
    - [Json.\*.Extra](https://package.elm-lang.org/packages/elm-community/json-extra/latest/)
    - [Array.Extra](https://package.elm-lang.org/packages/elm-community/array-extra/latest/)
      Provides helper to make an Array mutable, to zip, slice it and resize.
    - [Basics.Extra](https://package.elm-lang.org/packages/elm-community/basics-extra/latest/)
      Provides helpers to swap function arguments (swap, flip, curry, uncurry), ensure an interger
      carries a safe value and some geometry functions.
    - [Ease](https://package.elm-lang.org/packages/elm-community/easing-functions/latest/)
      Provides helpers to compute fade in, fade out and other fx.
    - [Maybe.Extra](https://package.elm-lang.org/packages/elm-community/maybe-extra/latest/)
      Provides various helpers that works around hypothetical results, when the equivalent
      function requires a strict input.
    - [String.Extra](https://package.elm-lang.org/packages/elm-community/string-extra/latest/)
      Helpers to doctor string content (case sensitivity, variable naming standards, etc),
      butcher it, clean it, trim it, etc
    - [Graph](https://package.elm-lang.org/packages/elm-community/graph/latest/)
      <!-- TODO -->
    - [List.Split](https://package.elm-lang.org/packages/elm-community/list-split/latest/)
      Helpers to break a List of things into a list of chunks of things (with fixed size)
    - [Random.Extra](https://package.elm-lang.org/packages/elm-community/random-extra/latest/)
      Helpers to Randomness
    - [Result.Extra](https://package.elm-lang.org/packages/elm-community/result-extra/latest/)
    - [UndoList](https://package.elm-lang.org/packages/elm-community/undo-redo/latest/)
      Helps implementing Undo/Redo mechanism through the Msg system.
    - [Test me! test me!](https://package.elm-lang.org/packages/deadfoxygrandpa/elm-test/2.0.0/)
    - []()

* community extras
    - [Tuple2, Tuple3](https://package.elm-lang.org/packages/TSFoster/elm-tuple-extra/latest/)
    - [Set.Extra](https://package.elm-lang.org/packages/stoeffel/set-extra/latest/)
    - [String.Format](https://package.elm-lang.org/packages/jorgengranseth/elm-string-format/latest/)
      Limited Mustache formatted strings. I'm sadness :'(
    - [Unsigned integers](https://package.elm-lang.org/packages/ktonon/elm-word/latest/)
    - [Additional string content manipulation](https://package.elm-lang.org/packages/the-sett/elm-string-case/latest/)
    - []()

    - [Xml parser](https://github.com/stkb/elm-xml-parser/tree/master/src/Xml)

## How to

- [How to Form](https://www.oreilly.com/learning/how-to-do-client-side-form-validation-with-elm)
- [How to parse JSON in Elm](https://javascriptplayground.com/json-decoding-in-elm/)
- Use Json.Decode.Pipeline instead of Json.Decode.map unreadable crap
- How to get remote data: Http.send or RemoteData
- How to [import and alias modules](https://blog.codecentric.de/en/2015/12/elm-friday-part-08-imports/).

# Plumbing

## Package management

Tool | Desc
--- | ---
nodejs        | The runtime server-side
npm           | the official tool to install NodeJS modules<br>DO NOT use! It conflicts with Yarn.
yarn          | tool used to manage NodeJS modules
elm-package   | tool to install ELM modules/package

### Remove a package

You have to do it manually. First, you have to remove it from `elm-package.json`, then you
rebuild the Elm stuff:

```bash
rm -rf elm-stuff
elm-install -y
```


## Serving app alternatives

elm-reactor                                 | A simple web server to compile and serve Elm apps on the fly
[webpack](https://webpack.js.org/concepts/) | A local (?) NodeJS web server
json-server                                 | <!-- XXX -->

## Webpack

Config file: `$project/webpack.config.js`


Webpack aims to automagically find dependencies to your app. current used version isn't so
wizardy, so we have to tell it:

  - which script is the *entry* point `module.exports.entry`
  - where and how to cache the *output* of the processed app `module.exports.output`
  - how to integrate files, using *loaders* `module.exports.module.rules`. The role of a
    loader is to generate a valid JS file from the input file. It may transform the
    content to embed it.
  - how assets are fetched or content is bundled, using *plugins*.
  - the operating mode (production, development)

### Webpack plugins

[webpack-cli](https://webpack.js.org/api/cli/)      | A development tool to help a developer in its daily tasks
webpack-dev-server      | Plugin to provide developer facilities
webpack-elm             | Plugin to support Elm
[css-loader](https://github.com/webpack-contrib/css-loader) | A webpack loader to build and serve CSS files
[file-loader](https://github.com/webpack-contrib/file-loader) | A webpack loader to integrate raw files
[style-loader](https://github.com/webpack-contrib/style-loader) | A webpack loader to serve stylesheets (to be used with css-loader)
[url-loader](https://github.com/webpack-contrib/url-loader) | A webpack loader to issue a file as an inline content URN

[font-awesome](https://github.com/FortAwesome/Font-Awesome) | SVG, font, and CSS toolkit 
[ace-css](https://github.com/basscss/ace) | Provide access to [Basscss](http://basscss.com/).

Basscss is a subset of CSS implemented as classes. With no namespaces. Holy bullshirt.

# DON'T

Don't use those packages:

- Don't use tuple over 2 elements (undefined behaviours ahead)
- This [XML parser](https://package.elm-lang.org/packages/eeue56/elm-xml/latest/) isn't
  complete, as it isn't possible to access attributes.
- [XMLParser](https://package.elm-lang.org/packages/jinjor/elm-xml-parser/1.0.0/) isn't
  fully featured

# Gotchas

- Beware of type shadowing. Defining a type with a name already in use won't trigger any warning.
