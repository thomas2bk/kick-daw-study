# License boundary

Upstream `MusicTribeOpenSource/0700-AAM` Music Tribe code (Kick, AudIO, ComProtocol) is **AGPL-3.0-or-later**. Linux Buildroot is GPL-2.0; bundled third parties keep their own licenses. Behringer / KICK names are trademarks.

## This study repo may

- Quote short factual excerpts for criticism / interoperability analysis  
- Redescribe architecture in original prose  
- Compare public APIs and folder layouts to MPCX docs  
- Link to upstream commits and READMEs  

## This study repo must not

- Vendor AGPL trees into git history (see `.gitignore` `vendor/`)  
- Copy substantial Kick / AudIO / ComProtocol source into MPCX  
- Ship modified KICK firmware as if it were MPCX  

## If someone wants to hack on KICK itself

Work in a **fork of upstream** under AGPL obligations (network use / corresponding source rules apply). Keep that work separate from MPCX’s license.

## Snapshot pin

Analysis written against upstream commit:

`27194180ce5fbab3776ebce53e2d4b016597364e` (2026-10-15)
