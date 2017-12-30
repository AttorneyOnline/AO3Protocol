Overview
--------

All assets must contain these two files: `info.json` and `content.tar`.

`info.json`:
```javascript
{
   id: string
   (parent: string)
   name: string
       // Use spaces, not underscores. This is not an internal name
       // and should never be used as if it were a unique identifier.
   hash: string
       // By default, a sha1 hash of content.tar.
   (hash_type: string)
       // Not implemented yet.
   author: string
   date: string (ISO-8601)
   category: string (see below for valid categories)
   size: integer
}
```

Categories tell Animated Chatroom how the assets should be organized.
Game-specific data can also be placed under sub-categories (such as `ao3/evidence`).

We must also explain what content must be placed inside `content.tar` based on the asset's category.

### Characters
Category: `character`

Contains a `manifest.mp` file which is encoded with MsgPack.

`manifest.mp`:
```javascript
{
    icon: string (filename)
    (blip: string)
        // If none is selected, the default sound will be used.
    emotes: ordinal set of emotes [
        {
            name: string
            icon: string
                // The path to the icon for the button.
                // Recommended 64x64 or 128x128.
            idle: animation
            talking_preanim: animation
                // Another preanimation before this one can be chained by
                // the user.
            talking: animation
            talking_postanim: animation
        }
    ]
    preanims: ordinal set of preanims [
        {
            name: string
            icon: string
            animation: animation
        }
    ]
    animations: {
        [name]: string (apng, gif, or webm filename)
    }
    ao3: {
        side: enum {
            WITNESS = 0
            DEFENSE = 1
            PROSECUTION = 2
            JUDGE = 3
            // don't remember what these stood for...
            HLD = 4
            HLP = 5
        }
        (objection_override: {
            hold_it: string (filename)
            objection: ...
            take_that: ...
            custom: ...
        })
    }
}
```

The remainder of the archive contains animation files.

### Backgrounds
Category: `background`

`manifest.mp`:
```javascript
{
    sides: ordinal set of sides [
        {
            name: string
            animation: string (animation filename)
        }
    ]
    overlays: [string]
}
```

### Audio
Category: `audio`

Only holds one audio file at a time for a few reasons:
 1. I don't want people hosting entire music albums.
 2. The format will be misunderstood, causing great confusion and duplication across servers.
 3. It makes adding new audio files on-the-fly significantly easier.

`manifest.mp`:
```javascript
{
    filename: string
    length: float
}
```

### Evidence
Category: `ao3/evidence`

`manifest.mp`:
```javascript
{
    images: [string]
}
```
