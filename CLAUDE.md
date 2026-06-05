# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository contains a single [Brave Search Goggle](https://search.brave.com/help/goggles) for the Kanton Solothurn career path project (Squirro). A Goggle is a declarative filter/reranking rule file that customizes Brave Search results.

There is no build system, no tests, no dependencies, and no executable code — the project is a single `.goggle` configuration file.

## Goggle File Format

The active file is `solothurn-career-path0.0.2.goggle`. The version is embedded in the filename.

**Syntax conventions:**
- Lines starting with `!` are comments or metadata headers (`! name:`, `! description:`, `! public:`, `! author:`)
- `$discard` as a standalone instruction sets the default behavior to remove all results not explicitly matched
- URL patterns use `*` as a wildcard (matches any character including subdomains and path segments)
- `$boost=N` appended to a URL pattern raises the ranking weight of matching results (higher = stronger boost)
- Rules are processed top-to-bottom; later rules can override earlier ones

**Current whitelist logic:**
```
$discard                                              ← discard everything by default
*karriere.so.ch/*$boost=10                            ← keep all pages on karriere.so.ch
*karriere.so.ch/stellenmarkt/offene-stellen/*$boost=10  ← keep open positions (redundant but explicit)
*so.ch/verwaltung/finanzdepartement/personalamt/*$boost=10  ← keep Personalamt pages
```

## Versioning Convention

When making changes, rename the `.goggle` file to increment the patch version (e.g. `0.0.2` → `0.0.3`) and update all references to the filename in `README.md`.

## Installation

Paste the raw GitHub URL of the `.goggle` file into the [Brave Goggles dashboard](https://search.brave.com/goggles). Brave fetches and caches the file from that URL.
