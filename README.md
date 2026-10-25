# Deprecated

**Do not use this.** It has been superseded and is kept only so the history stays
readable.

## What it was

A copy of [magpie-community/plugins](https://github.com/magpie-community/plugins)'s
`registry.json` with my own entries appended, served so that
`MAGPIE_PLUGIN_MARKET=<url>` could make those cards complete.

## Why it is wrong

It is the same idea as self-registration, with two extra costs and no benefit:

| | Self-registration (in the plugin) | This repository |
|---|---|---|
| Configuration | none | an environment variable |
| Where the entry goes | magpie's own cache | a copy of the list |
| Maintenance | none | a repository and a workflow |
| Survives magpie's refresh | re-applies within 500 ms | not applicable |

A plugin can merge its own entry into the cache magpie already keeps. The template
does exactly that:

https://github.com/MYCF711/magpie-plugin-template/blob/main/src/self-register.mjs

## What should replace all of this

The underlying problem — magpie replaces its plugin list wholesale, so a package
outside it can never keep a complete card — is written up here:

https://github.com/magpie-community/plugins/issues/394

The smallest fix suggested there is for the fetched list to merge into the cached one
rather than replace it. One write from a plugin would then be enough, and neither
this repository nor the watcher would be needed.
