# API Blueprint to OpenAPI

Migrate API Blueprint to OpenAPI v3.1 with a few different tools that have been
glued together to make a surprisingly good result. 

## Why would we need that?

Apiary, the company behind API Blueprint, was acquired by Oracle a while back
and now they're closing their doors for good. API Blueprint has therefore been
left abandoned, so it's time to hop on over to the OpenAPI ecosystem. Ideally
you'll use this repo to help migrate, then never look back.

## How it works

Clone this repository, and replace `original.apib` with your API Blueprint
downloaded from Apiary or wherever it happens to live.

```shell
git clone git@github.com:bump-sh-examples/apiblueprint2openapi.git

cd apiblueprint2openapi

cp ~/src/my-project/example-api/latest.apib ./original.apib
```

With this in place, run NPM installer as all the best/latest/current tooling for
this happens to be JavaScript based.

```shell
npm install

npm run convert
```

The conversion script should create a few files in `generated/`, with output
from two different conversion scripts so you can see which you prefer.

- `apib2openapi.yaml` - Using NPM module `apib2openapi` to produce OpenAPI v3.0.
- `apib2openapi.31.yaml` - Upgraded `apib2openapi` output with `openapi-format` to produce OpenAPI v3.1 and generally tidied up.
- `apispecconverter.yaml` - Using NPM module `apib2openapi` to produce OpenAPI v3.0.
- `apispecconverter.31.yaml` - Upgraded `apib2openapi` output with `openapi-format` to produce OpenAPI v3.1 and generally tidied up.0.

This is probably a lot to think about so to keep it simple, **you probably want to
use `generated/apispecconverter.31.yaml`**.

```shell
cp generated/apispecconverter.31.yaml ~/src/my-project/example-api/openapi.yaml
```

## Preview OpenAPI

Want to see how they look with zero effort involved? 

```shell
$ npm exec bump preview generated/apispecconverter.31.yaml

> Your preview is visible at: https://bump.sh/preview/9b563ce6-e1a5-4da6-8f5d-d51ae0b26c1d (Expires at 2025-06-27T17:49:34+02:00)
> * Let's render a preview on Bump.sh... done
```

## Underlying Tools

This conversion process is using a few different tools. 

- [LucyBot API Spec Converter](https://github.com/LucyBot-Inc/api-spec-converter) - A 
  JavaScript library we're using to convert API Blueprint to OpenAPI v3.0.
- [apib2openapi](https://www.npmjs.com/package/apib2openapi) - A JavaScript
  library that converts API Blueprint to OpenAPI v3.0.
- [OpenAPI Format](https://www.npmjs.com/package/openapi-format) - A JavaScript
  library that formats OpenAPI documents to be more readable and to upgrade
  OpenAPI v3.0 to v3.1.
- [Bump.sh CLI](https://www.npmjs.com/package/bump-cli) - Renders OpenAPI
  documents as a preview, so you can see how they look without having to run a
  local server.

## Customization

Using OpenAPI Format was particularly helpful, as all of the conversion tools alone were generating unhelpful output, with invalid `operationId`. OepnAPI Format allowed us to override the `operationId`, using customizations in the `config/openapi-format.js` file. See more customization options in the [OpenAPI Format documentation](https://github.com/thim81/openapi-format?tab=readme-ov-file#openapi-formatting-configuration-options)
