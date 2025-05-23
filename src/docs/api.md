---
title: API Reference
description: The API reference is a detailed documentation of all the endpoints available in the SVGL API.
---

<script>
  import Endpoint from '../components/endpoints.svelte';
  import Alert from '../ui/alert/alert-component.svelte';
</script>

## Introduction

SVGL API is a RESTFul API that allows you to get all the information of the SVGs that are in the repository.

## Limitations

The API is currently open to everyone and does not require any authentication. However, to prevent abusive use of the API, there is a limit to the number of requests.

<Alert type="info">
  Don't use the API for create the same product as SVGL. The API is intended to be used for extensions, plugins, or other tools that can help the community.
</Alert>

## Base URL

The base URL for the API is:

```bash
https://api.svgl.app
# or
https://api.svgl.app/categories
```

## Typescript usage

- For categories:

```ts
export interface Category {
  category: string;
  total: number;
}
```

- For SVGs:

```ts
export type ThemeOptions = {
  dark: string;
  light: string;
};

export interface iSVG {
  id?: number;
  title: string;
  category: tCategory | tCategory[];
  route: string | ThemeOptions;
  wordmark?: string | ThemeOptions;
  brandUrl?: string;
  url: string;
}
```

- `tCategory` is a large list of categories that can be found [here](https://github.com/pheralb/svgl/blob/main/src/types/categories.ts#L1).

## Endpoints

<Endpoint title="Get all SVGs" method="GET" description="Returns all the SVGs in the repository.">

```bash
https://api.svgl.app
```

<p></p>

```json
// Returns:
[
  {
    "id": 0,
    "title": "Discord",
    "category": "Software",
    "route": "https://svgl.app/discord.svg",
    "url": "https://discord.com/"
  },
  ...
]
```

</Endpoint>

<Endpoint title="Get a limited number of SVGs" method="GET" description="Returns a limited number of SVGs in the repository. Start from the first SVG.">

```bash
https://api.svgl.app?limit=10
```

<p></p>

```json
// Returns:
[
  {
    "id": 0,
    "title": "Discord",
    "category": "Software",
    "route": "https://svgl.app/discord.svg",
    "url": "https://discord.com/"
  },
  ...
]
```

</Endpoint>

<Endpoint title="Filter SVGs by category" method="GET" description="Returns all the SVGs in the repository that match the category.">

```bash
https://api.svgl.app/category/software
```

<p></p>

```json
// Returns:
[
  {
    "id": 0,
    "title": "Discord",
    "category": "Software",
    "route": "https://svgl.app/discord.svg",
    "url": "https://discord.com/"
  },
  ...
]
```

The list of categories is available [here](https://github.com/pheralb/svgl/blob/main/src/types/categories.ts) (except for the _all_ category).

</Endpoint>

<Endpoint title="Get only categories" method="GET" description="Returns only categories with the number of SVGs in each category.">

```bash
https://api.svgl.app/categories
```

<p></p>

```json
// Returns:
[
  {
    "category": "Software",
    "total": 97
  },
  {
    "category": "Library",
    "total": 25
  },
  ...
]
```

</Endpoint>

<Endpoint title="Search SVGs by name" method="GET" description="Returns all the SVGs in the repository that match the name.">

```bash
https://api.svgl.app?search=axiom
```

<p></p>

```json
// Returns:
[
  {
    "id": 267,
    "title": "Axiom",
    "category": "Software",
    "route": {
      "light": "https://svgl.app/axiom-light.svg",
      "dark": "https://svgl.app/axiom-dark.svg"
    },
    "url": "https://axiom.co/"
  }
]
```

</Endpoint>
