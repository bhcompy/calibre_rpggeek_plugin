# RPGGeek Metadata Source Plugin for Calibre

## Overview

This is a plugin for [Calibre](https://calibre-ebook.com/) that searches for book metadata from [RPGGeek](https://www.rpggeek.com/).

Mapping from rpgitem:
| RPGGeek  | Calibre |
| ------------- | ------------- |
| name (primary)  | Title  |
| rpgdesigner  | Author(s)  |
| rpggenre  | Tags  |
| rpgseries  | Series  |
| rpgpublisher  | Publisher (1st only)  |
| yearpublished  | Published  |
| description  | Comments  |
| image  | Cover  |

Limitations:
- rpgpublisher is not ordered.  This only pulls the first publisher.  Something to explore for a future release linking to rpgitemversion (rpgitemversion does not include publisher data, which is unfortunate)
- yearpublished is only a year.  RPGGeek does not store a full release date.  Defaults to yyyy-01-01.  rpgitemversion includes ISBN.  Future release to explore pulling ISBN to provide complete date
- Languages is not set.  Would come from rpgitemversion once built
- image pulls the primary cover, not version cover.  Would come from rpgitemversion once built
- Not every item has a series.  Originally intended to group by RPG system for use with Kavita as Series, but this seems too restrictive if a Kavita library is organized by system already.  Series instead pulls from rpgseries, which is more oriented around modules.  For instance, Kingmaker Adventure Path (PF2) has a series of Kingmaker and a series of Pathfinder Adventure Path.  It pulls the first series only (as Calibre and Kavita both only support one).

Future Considerations:
- rpgitemversion support (cover, publisher(s), date, language by version)
- Setting and Category included in tags

## Develop

Requirements:
- Python
- Calibre


```
git clone https://github.com/kovidgoyal/calibre.git

git clone https://github.com/bhcompy/calibre_rpggeek_plugin.git
cd calibre_rpggeek_plugin
python -m venv .venv
.venv/Scripts/activate
pip install -r requirements.txt
```

In .venv/Lib/site-packages, create a file Calibre.pth.

In that file, enter {path to where you cloned Calibre}/src.

### Test

```
calibre-customize -b .
calibre-debug -e test.py
```
