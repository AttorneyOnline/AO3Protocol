Animated Chatroom
=================

a project


-----------------


# Preface

This preface is a personal account the events surrounding the formation and
development of Attorney Online, the fan-made game that serves the impetus
behind Animated Chatroom (which I will henceforth refer to as "AC").

In 2012, there existed a case-making site called
[Ace Attorney Online](http://aaonline.fr), (at the time, it was located at
http://aceattorney.sparklin.org). The fan-made site grew to be successful:
allowing players to create their own cases faithful to the style and flow
of Ace Attorney, a plethora of such cases were made and could be played
by anyone. It is certain that Ace Attorney Online attracted new players
to the franchise; as such, legal recourse was never taken by Capcom.

In 2013, a Russian fellow named FanatSors decided to write a fan-made game
of a similar intent, but with an entirely opposite execution. Dubbed
"[Attorney Online](http://attorneyonline.tumblr.com/)," the game was written
in Delphi and did not support offline cases; rather, it encouraged the players
to play out their own cases impromptu, following a looser format in comparison
to the formulaic case format of Ace Attorney Online. In essence, AAO strived
to be a simulator, whereas AO strived to be a chatroom.

In addition to YouTube videos recording the hilarity of case derailments in AO,
Fanat further publicized his game by creating "Turnabout Storm," a series
which crossed over the *Phoenix Wright* saga with *Professor Layton* and
*My Little Pony*. A moderate success, it was enough to bring the attention
of my brother in 2015, approximately one year following the release of 1.7.5,
the final version of AO.

Personally, while I was not interested in the cases, as I had little time to
sit through the drawn-out dance of roleplay, I was intrigued by the technical
limitations of AO and sought to modify the game to add features, such as a way
of automatically downloading assets instead of having to manually download them
from every server by dumping a ZIP file onto a folder aptly named "base."

I invested a considerable amount of time in the summer of 2015 to attempt to
reverse engineer the AO client. However, I knew little about reverse
engineering, and I found that decompilation of Delphi executables to Delphi
source was essentially impossible, as I had originally believed that Delphi
used a bytecode (akin to Java). Desperate for source code, I asked wherever I
could, yet no response was given. Burnt out from a fruitless project, I finally
met stonedDiscord, a German fellow who wrote an open-source AO server (dubbed
"serverD") written in PureBasic. As it turned out, he had already attempted to
reverse engineer the AO client far before I even entered the scene, also having
yielded few results from his efforts.

This caused me to look broader: what if the solution was to remake AO? It would
be open-source, extensible, and contributable by anyone who wished to pitch in.
But alas, like any of my other projects, it was simply too ambitious to ever
consider being finished, especially if I was the sole contributor. With school
and other, smaller projects in mind, I set AO to the corner of my mind and
proceeded on with my life. Meanwhile, my brother grew bored of AO and moved the
group that he had assembled from AO over to Roll20. (To this day, he still
roleplays in Roll20 with around twenty other people in the group, and is still
known by his excellent roleplay of Professor Layton.)

About a year later, I decided to take a quick peek at state of AO again: how
was this game doing? Was it dead yet? What kind of people were still playing?
Surprisingly enough, I found not only a considerable number of people online,
but also a remake being worked on by a Norweigan fellow named OmniTroid. Dubbed
"Attorney Online Remake" (and later "AO2"), the project was being written in
C++ using the Qt library. I thought little of the project, however, knowing the
ramifications of such a massive undertaking. He is not going to finish, I
thought. I scoffed a little and moved on with my life once more.

About six months later, the same "quick peek" impulse occurred. I checked back
at this so-called remake, and taken aback, I found it at a formidable state. It
was essentially complete.

I took interest almost immediately after this realization. I wanted to reach
this OmniTroid person and tell them about my interest in working on the remake.
In Feburary of 2017, in anticipation of the release of "AO2," he established a
Discord channel. I frequented it for the next few months, and after a few weeks
of prying at the code and trying to make pull requests and issues wherever I
could, Omni finally took attention of my eagerness to contribute to the
project, granting me contributor access to the project and a developer role.

My first point on the agenda was a redesign of the asset system. After writing
a design document regarding the subject and waiting a few days, he vehemently
refuted my design, citing that it was too complicated, and the area was not
important enough to address. I felt tempted to "be a rebel" and fork the code
to implement the redesign myself, but before I even had the opportunity to
start on the implementation (I was extremely busy at the time), Omni invited me
to a private group with sD after asking me if I knew how to transfer a domain.
It was July 8, 2017, a week after my surreal trip to Japan.

I did not really know what this secret meeting was about. It was clear that
Omni desired to delegate to me control of more parts of the AO infrastructure
(which he had established after the death of Fanat-controlled master servers
and website), but why he decided to execute this *now* remained unclear.

I went through the migration process as he instructed. Service after service,
nearly everything was handed over to me: website DNS records, the GitHub
organization, the Discord server, and even the master server source code (which
seemed to be hastily written in Python, and, to his admittance, was mostly held
together by security-by-obscurity; to give you an idea, the script allocated
one thread for each and every client).

At the conclusion of the migration process, I began to realize what was going
on: Omni was leaving the project. A few minutes after I realized this, he said,
"I'm sure you'll figure it out... gl hf" and left the group. In a desperate
attempt to confirm my prediction, I tried to contact OmniTroid privately, but
no response came from him until much later. (When I was in Japan, I had been
given an administrator role in the Discord server as well, which was around 200
members strong).

The next few weeks were stressful. sD and I had to rebuild the AO
infrastructure, slipping off old components like Jenga blocks and replacing
them with new ones, all while preventing any marked collapse, such as the
website going down or the master server suddenly dropping. I took the next few
weeks to write a new master server that would replace Omni's old code, racing
against the clock to get it to working condition before he inevitably shut it
down. In a stroke of luck, I brought the new master server to a working state
and set it to standby a mere few days before Omni finally pulled the plug on
the master server. The migration was fairly smooth, and an hour after receiving
the first notifications of servers not appearing on the list due to the
shutdown event, the new master server was set up, fixed a few times, and set as
the default master server.

The conception of Animated Chatroom indeed began with the design of the
replacement master server. The master server project had taken me longer
than expected due to an intention to abstract the server to accommodate
AO1, AO2, and future AO clients, which I expected would use Protobuf
as a network protocol (since I vehemently despised Fanat's protocol and its
use of ASCII characters to delimit packets).

By late August, I was already thinking of concepts and design that would
drive Animated Chatroom, as well as reasons why AO2 simply could not be
continued further. The source code simply was too messy to add new features
to; moreover, there seemed to exist a number of difficult-to-trace memory leaks
(a side effect of using C++ as if it were Java, I suppose).

In the beginning of my administration of the new AO community, I had prospects
of merging with Visual Novel Online (VNO), a project developed by Fiercy,
Cronnicossy, and FanatSors as an alleged "successor" to AO. It was also written
in Delphi and likewise reverse engineered (albeit successfully) by sD. I
relished the idea of a community that would use the same software for an
all-inclusive variety of franchises; indeed, AO2 was being customized for
role-playing games that had nothing to do with Ace Attorney, such as
Danganronpa.

However, this idea of merging with VNO was not received well by anybody at all,
due to my poor understanding of the composition of the VNO community. The two
communities were wholly incompatible, and even Cronnicossy consoluted me in
rejection of this idea. I quickly dropped it and continued my gaze on Animated
Chatroom.

Sometime during my rediscovery of AO, I also learned of the so-called "AO 1.8,"
an unofficial update to 1.7.5 that made modifications to the default theme and
vanilla assets, as well as included an "Automatic Attorney Utility," a robust
set of macros for the game, since obviously the Delphi code could not be
modified. I had briefly considered writing master server code to "federate"
with the 1.8 master server, but I quickly abandoned the code after I realized
that the 1.8 master servers were long dead. Mine was virtually the only one
left standing.

During the fall semester, things were fairly uneventful. I was too busy to deal
with Animated Chatroom, although I would go to the lab computers every Friday
or so to work on some code or UI.

In December, during Christmas break, things predictably began to accelerate.
What I did not predict, however, was an old friend's sudden interest in my
Animated Chatroom project. Initially, he condemned me for my entire design and
thought process being convoluted since the solution was "so simple," but after
a few days of getting him up to speed and explaining why such and such was not
a plausible solution due to a fundamental problem (following about the same
line of thinking I had followed in the last six months), he finally was able to
understand the justification behind Animated Chatroom. While I felt a tension
between me and him due to his oversimplification of design objectives, we were
nevertheless able to accomplish work on a Python client and C# server.

Following the break, however, things decelerated once more. The friend wished
to place a deadline on "AO3," but I implored him that there would be absolutely
no promises attached to this project, lest I break one and be humiliated
eternally.

In February, my friend and another apparent developer had other plans: they
wished to make an Electron-based client for AO3, and they would make it
strictly for Attorney Online - it would not bear the name "Animated Chatroom."
After a while of debate, I reluctantly agreed to help them, while denying that
AC was cancelled. I wished to work on AC, but still could not find time.

From the blurs of development, it has come to my attention that the design
principles behind Animated Chatroom have not been unilaterally addressed. The
purpose of this document is to serve as an up-to-date reference of the
technical and ideological facets of the software. (After all, one must remember
that the AO community focuses itself around little more than a piece of
software; remove it, and there is hardly anything left that holds the community
together.)

Notwithstanding the ultimate fate of AC, I write this document in hopes that it
may serve useful for anyone who decides to take up this idea, although I
personally tend to doubt it as well. Many parts of the design have undergone
extensive debate; it would be wise to think of any problems before deviating
from what has been written here.



# Overview

## Purpose

The purpose of Animated Chatroom is to allow players to use sprites to
communicate with each other as if it were a visual novel, but without any
specific objective or goal. The sprites can be from any game or creative work,
and the program provides enough versatility to allow for complex situations to
be played out.

## Platform

The platform must be cross-platform and relatively slim. A bare install of AC
should be less than 75 MB. The size of any required runtimes must also be
factored into the size calculation.

### Python

Python is a very friendly language and has proven to have a favorable learning curve
for beginners and professionals alike. As a result of its reputation, many bindings
and libraries exist for it, including PyQt5 and FFmpeg.

### Electron

Electron is a glorified wrapper for Chrome Embedded Framework (CEF), allowing
OS calls while allowing the user interface to be written in standard HTML, CSS,
and JavaScript. It is relatively recent in development, and its reputation
remains to be established. Applications such as Atom and Discord use Electron.

If an Electron approach is taken, it is also advisable to keep a branch of the
code for use in browsers (without the need of Electron).

### Browser-based

Since the inception of HTML5, the browser has transformed from merely a layout
engine to an entire application platform. As such, it is becoming increasingly
easier to develop native-like applications for the browser.

Moreover, browsers come with WebM, GIF, APNG, Opus, and such resources can be
loaded and played back very easily with JavaScript.

Some unsolved problems remain with this approach, however:
 - Filesystem emulation using IndexedDB is not very well supported;
    as such, it may take more work to allow asset packages to be
    loaded in and extracted using browser-based JavaScript.
 - The DOM is slow to update, and browsers generally do not guarantee
    timing. This means that the window can stutter at any moment.
 - Browsers tend to be memory hogs; about 200-400 MB could be allocated
    for every open tab.
 - Inter-tab/process communication is difficult to manage.
 - Multi-clienting is difficult, since information is redundant across tabs.

If AC was less complicated, it could work on a browser. However, some features
are desired by power users that cannot be replicated on a browser, such as
certain hotkeys, as well as placing widgets across multiple monitors.


# User interface

The user interface should follow this basic hierarchy:
 - Each server occupies a main window.
 - Each room within a server occupies a detachable tab.
 - Each character occupied within a room occupies an in-character (IC) chat
    widget.

In addition to this hierarchy, almost every widget should be detachable from
the main window, with the exception of the viewport.

Due to the convenient ability to edit UI via Qt Creator, it is very easy to
customize the user interface. However, modders must be aware that additions
to the UI in future versions may cause problems.

## Lobby window

By default, this window should be shown on startup.

### Server list (left pane)

There are two tabs: master server list and favorites list.

Servers are sorted by player count. Each item in the table contains the name,
player count, protection level, and country of the server.

Servers can be easily added to favorites from the master list. Direct connect
is also supported.

If a player selects a server already connected to, the respective window is
focused and a "select room" dialog appears in anticipation of multiclient mode.

### Server information (right pane)

The information on the server's item is repeated, although more verbosely.
The description is also shown, as well as the designated URL of the server.

## Options

Options are mostly implementation-specific. For the purposes of this documentation,
however, I will refer to options that would be most appropriate for a Python-based
implementation.

Moreover, an options window is an excellent way to introduce feature creep to a
program. Options should never be introduced unless they have a legitimate use
case and have been requested by a significant amount of users. For this reason,
I will keep the options list short.

### Name

The default name of the player.

### Default asset repositories

The initial default asset repository should never be allowed to be deleted, in
case of an accident.

### Download custom assets by default

Some servers may allow players to bring their own assets into a server.
By default, these assets will not be downloaded automatically because they
may not be safe and can quickly accumulate in the local asset cache.

State the risks of allowing such automatic downloads when the "Yes" button
is selected.

### Scaling option

An illustration and extended description should be provided for each of the
scaling modes.

## Asset list

This is essentially a frontend to the database backing the asset cache.

There should be three options:
 - forced downloading of an asset (add),
 - removing an asset (delete), and
 - pruning old assets not used in the last user-specified
    number of days (prune).

## Loading dialog

The loading dialog should be modal to the lobby. A progress bar should be shown
along with a description. See the handshake process in the network
documentation for a detailed explanation of what may occur here.

Loading should be cancelable at any time during the process, although immediate
cancellation is not guaranteed.

### Asset downloads

An additional progress bar displaying the download progress for each individual
asset should be shown, as well as the name of the asset being downloaded.

## Main window

### Join sequence

When a main window is opened, the lobby window should be closed if the origin
was from the lobby. (It can then be reopened via `File -> Show Lobby` or some
related sequence.)

The player is immediately asked to select a room. After a room is joined,
the player is asked to select a character. If the process completes
successfully, the main window's widgets then become accessible.

### Room selection dialog

Each room is listed with a title, number of players, protection status,
and description. Canceling this dialog when there is no active session
causes a disconnect.

### Character selection dialog

In the grid layout, only the character's icon is shown, and the character's
name is shown on hover. If it is allowed, a button at the bottom named
"Custom..." allows the player to search for a character in the asset cache.

### Viewport

This is the central widget of the main window. As a result, it cannot be moved
out of the main window. See the Core section for more information on how it
works.

### In-character (IC) chat widget

This contains an adaptively resized chat box, as well as a grid view of
available emotes, preanimations, and interjections for a character.

In the future, the chat box may provide auto-completion for the markup language
stipulated in the Core section. It may also provide support for buffers
in the future.

### IC log

This is simply a log of everything said in the IC log up to a certain point in
time (e.g. last 5 minutes of server chat, chat since player joined, etc.)

### Out-of-character (OOC) chat widget

This contains an adaptively resized chat box, as well as a bare-bones chat log.

### Jukebox

This is a searchable tree view of the music assets available on the server.

### Player list

This is a list of players currently in the room. If the server allows it,
the character(s) associated with each player is also shown in a tree hierarchy.

If admin permissions are available, right-clicking a user or character will
allow kicking.

### Sound mixer

This provides a list of sound channels and faders/monitors for each of them.
However, managing sound is troublesome due to the need for privilege
management and such, so this widget is optional.

## Server console

It may be possible to create a listen server from within AC, so a server
console should be implemented. Moreover, it eliminates the need to recreate a
separate server UI for dedicated server implementations.

### Key-value list

This is simply a frontend to the settings list of the server.

### Migration button

For listen servers only: a host may decide to hand over control of the server
to another player. The host must wait until the player accepts or denies the
request, as this is a modal dialog. See the Network section.

# Assets

The asset system is loosely based on version 1 of the Docker container format,
an uncomplicated format compared to subsequent versions. Although it seems
ridiculous to base a small package format from a container format, I took
this decision based on the necessity that differences between assets should be
as small as possible. In many cases, modders tend to make derivatives of assets
with very few differences between them, but where there exists a parent-child
hierarchy, we can save space. This is basically the core idea that was taken
from the Docker format; any other complexities were disregarded.

There are some large use case differences, however, that otherwise render the
Docker format impractical for adoption as a model:
- Files within an asset do not need to be marked for deletion; they are simply
    left unused. (Besides, their method of tagging files for deletion seemed
    likely to collide with real files.)
- The tar format assumes that all files will be extracted in sequence; in
    reality, this is not the case. We may only need to seek for one file.
    Most implementations of tar assume a sequential read of the archive
    to find a file, even though the extended tar format includes an index.

## Format

Every asset is uniquely identified in a consistent format. We shall define this
format to be the SHA-256 of the archive file.

The archive file is a ZIP file that contains all information about the asset in
a manifest file, along with accompanying data.

### Manifest

The manifest file, named `info.json`, is a file that describes the asset
and refers to files that are part of this asset or parent assets.

Chunks of a sample manifest are included below. The latest sample may be
found in the fantaconvert repository. Fields starting with an underscore may
be ignored, as they are purely informational (JSON does not allow comments).

#### Header

Required in all assets.

```json
{
  "name": "Adachi",
  "category": "character",
  "_category_options": [
    "audio",
    "background",
    "character",
    "evidence",
    "meta"
  ],
  "parent": "optional",
  "meta": {
    "author": {
      "name": "required if author field is included",
      "url": "optional"
    },
    "desc": "optional",
    "source": "[wikidata]",
    "date": "ISO-8601"
  }
}
```

#### Characters

```json
{
  "chatbox_name": "optional",
  "side": "pro",
  "_side_options": [
    ["wit", "Witness"],
    ["def", "Defense"],
    ["pro", "Prosection"], 
    ["jud", "Judge"],
    ["hld", "Helper defense"],
    ["hlp", "Helper prosecution"]
  ],
  "icon": "char_icon.png",
  "blip": "blip.wav",
  "_blip_comment": "extracted from base installation",
  "emotes": [
    {
      "name": "Coat On",
      "icon": "emotions/button1_on.png",
      "idle": "(a)normal.gif",
      "talking": "(b)normal.gif",
      "zoom": true,
      "_zoom_comment": "not present if false"
    }
  ],
  "preanims": {
    "coat": {
      "anim": "precoat.gif",
      "duration": 60,
      "sfx": {
        "file": "cool.wav",
        "delay": 60
      }
    }
  },
  "interjections": [
    {
      "name": "Hold it!",
      "sound": "holdit.wav",
      "anim": "holdit.gif"
    },
    {
      "name": "Objection!",
      "sound": "objection.wav",
      "anim": "objection.gif"
    },
    {
      "name": "Take that!",
      "sound": "takethat.wav",
      "anim": "takethat.gif"
    }
  ]
}
```

## Packaging

The conversion of assets from the AO1 family (`char.ini` format) can be
accomplished using the fantaconvert tool.

Large formats, such as WAV and GIF, should be compressed to the target/ideal
asset format.

The resulting archive should be named either the unique ID of the asset, a
truncated version of the unique ID, or a combination of the asset name and its
unique ID. The actual name does not matter, so long as it cannot collide with
other archives. The internal databases of the client and server will internally
determine which assets correspond to which archives.

## File formats

This section is still under debate. The proposed formats are as follows:

- **Still images**: PNG
- **Animations**: WebM/VP8 (YUVA420P)
    We have determined that this is the only up-to-date format that supports
    8-bit transparency with compression that matches or exceeds that of GIF.
- **Sounds**: MP3 (128~192k) or Opus (96k)
    MP3 remains the "gold standard" for music compression. However, recent
    audio sampling tests indicate that Opus provides nearly transparent
    quality at a low bitrate (96k). To save on size and as a trial adoption
    of the Opus format, Opus should be used for small audio files and some
    music files. However, no transcoding need be performed if the file
    already exists in MP3 format.

## Repositories

Asset repositories are essentially file servers hosting assets. They are
decentralized; anyone can host an asset repository. Repository owners may
impose any kind of standard they wish on assets submitted to such repositories.
The minimum standard suggested is a similarity check, which is explained later.

Clients have a list of repositories they may download assets from. Clients
download an index of assets from each repository and try the first repository
that provides the asset. Servers may also offer a supplementary list of
repositories that may be used in tandem with the client's local list. The local
list always takes precedence over the server-provided list.

### Standard repository index

```json
["asset_id_1", "asset_id_2", ...]
```

### Mini-repositories

In consideration of most server owners who wish to create private assets being
unable to host entire repositories from their own networks, "mini-repositories"
allow server owners to place a repository index on a file-hosting website.
This repository index then lists assets and the URL to the ZIP file of each
asset.

```json
[{"id": "asset_id_1", "url": "https://dl.dropbox.com/s/..."}, ...]
```

The advantage to mini-repositories is that they can be stacked on a server
repository list; they need not be reconstructed for every update. For instance,
a server owner may generate a mini-repository for new ZIP files added in
monthly updates, and the new mini-repository does not need to include the ZIP
files from the previous months. The old mini-repositories are simply kept in
the list.

### Submission

Owners of public repositories should manually review submitted assets to
control quality across the entire system. The reference implementation
of the asset server should include a tool to thoroughly validate asset
manifests to ensure no foul play has been done and that the asset does
not already exist.

Due to the non-deterministic nature of the manifest (as a result of the
inclusion of a timestamp, as well as whitespace and ordering differences), it
is not possible to compare assets by a simple hash. Instead, the files within
the archive must be compared by hash, and then the manifest must be compared by
field, in order to generate a similarity percentage. (Since such comparisons
must be performed against possibly hundreds of assets, a database or cache
could accelerate the process.) If the highest similarity percentage calculated
is greater than 85%, this indicates that the asset is probably a duplicate of
another asset, and the parent of the submitted asset should be set to the asset
which was duplicated. The submitted asset will have to be sent back to the
submitter to make this correction.

After the manual verification, the repository owner may then place the asset
archive in the server's storage and refresh the asset server.

# Core

The core is the most interesting - and most challenging - piece of AC. There do
not exist any "true" online visual novel engines, those which promote
extensibility and abstraction.

Contrary to belief, it is more than simple animation, and it most definitely
requires more work than simply strapping a video player onto the game.
Timing *must* be considered as well as layering.

## Attempted solution: Visual Novel VM

My first attempt to create an abstract core was to make a VM called the "Visual
Novel VM," and then allow the server to emit VNVM bytecode to clients.
In this way, the work of the core would be eliminated from the client
perspective: it would be the job of the server to translate messages into
bytecode, which would get executed by clients. The state of the machine could
be tracked perfectly, allowing near-perfect synchronization and trivial
replay support using markers. I would also be able to get the headline for
"write your next visual novel in assembly."

A machine code concept is also employed in numerous released games. This
explains the ease of porting some *Ace Attorney* games from 3DS to mobile.

Despite the purported convenience, the scheme was seen as impractical and
complicated, so I decided not to pursue it any further.

## Messages

More to come.
