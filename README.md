# costar-data

The film dataset for **CoStar**, a daily movie-connection puzzle for iOS.

This repository exists so the app can refresh its film list without shipping an app update.
It is public for one reason: the app fetches `films.json` over plain HTTPS with no credential,
and a private repo's raw URL would require a token. A token in an app binary is a token you
have given away.

```
https://raw.githubusercontent.com/drdjcannon/costar-data/main/films.json
```

## What is in here

One file. `films.json` is generated, never hand-edited.

```json
{
  "version": 3,
  "people": [{ "id": "p_tom_hanks", "name": "Tom Hanks", "dailyCandidate": true }],
  "films":  [{ "id": "f_apollo_13_1995", "title": "Apollo 13", "year": 1995,
               "cast": ["p_tom_hanks"], "directors": ["p_ron_howard"] }]
}
```

- `version` must increase on every publish. The app accepts a remote dataset only when its
  version is strictly greater than the one it is running, so forgetting to bump it means every
  device silently ignores the update.
- `dailyCandidate` marks people who may be dealt as a daily puzzle pair. It is false for the
  many directors that come along with a film as a side effect. They are still real nodes in the
  graph and still browsable in the app; they are just not something the daily will ask you to
  connect.

## How it is produced

Generated from a hand-curated core merged with TMDB-sourced filmographies, filtered to
well-known theatrical features. The curation is deliberate: a complete credits dump connects
almost anyone in two steps, through documentaries, talk shows and award ceremonies, which
destroys the puzzle.

The generator lives in the CoStar app repository, not here. This repo is a publishing target.

## Attribution

This product uses the TMDB API but is not endorsed or certified by TMDB.

Film and cast data originates from [TMDB](https://www.themoviedb.org).
