# wormholeCypher

Work in progress!

Goal: A small HTML5 app that makes Cypher commands for Neo4j out of pasted text, copied from the EVE Online probe scanner and bookmarks.

The Cypher commands can be dropped into the Neo4j, the grap database, so you can get an overview of your journey in and out of wormhole space.

This app is just for fun.

## To Do

1. Write code to parse pasted bookmark-data
2. Write code that generate the Cypher commands, and print them out

The current app can already parse pasted signature-data and save it into a simple array of objects.

## App Installation

The actuall (unfinished) app, a simple HTML5 file containing just CSS, HTML and JavaScript (and some additional notes), is in the  `bin/` folder.

You will need a working version of Neo4j beforehand. Otherwise just download the HTML-file and open it in your favourite web browser to try it out. Feel free to fork or steal the code as per MIT license.

## Usage

### Probe Scanner Signatures

Mark all scanned signatures in-game.

Click the top sig.

Hit `[⇧ Shift]` and click the bottom sig.

(Or hold `[Ctrl]` and click the ones you've scanned thus far.)

Hit `[Ctrl]+[C]`

Click inside the text area above and hit `[Ctrl]+[V]`

Next copy-paste bookmarks.

This will add details to the existing signature object, before the Cypher commands are generated.

### Wormhole Bokmarks

Click the first correctly formatted bookmark.

Hold `[Ctrl]` and click the bookmarks for the other wormholes.

Hit `[Ctrl]+[C]`

Click inside the text area above and hit `[Ctrl]+[V]`

Important

Only accepts bookmarks that are very carefully formatted, like so:

`* - [entry-SIG] - [type] - [domain || system] - [exit-SIG]`

Example:

`* - XYZ - K162 - HS`

`* - XYZ - N770 - J153449 - NRE`

Legend:

`*` is mandatory. It means here is a wormhole

`-` is mandatory. It serves as separator for readability.

`[entry-SIG]` is a three letter signature code in the system you're in, or just came from.

`[type]` is the wormhole code, i.e. `K162` for an exit, or `U210` leads to lowsec, `B274` leads to highsec.

`[domain || system]` is mandatory. It's where you write what domain or actual system the wormhole leads to. Here are the possible domains:

- U: Unknown Wormhole
- D: Dangerous Wormhole
- C6: Deadly Wormhole
- NS: Nullsec
- LS: Lowsec
- HS: Highsec

The fourth `-` and the last `[exit-SIG]` are optional.

`[exit-SIG]` is the signature code for the other side of the wormhole, as it shows up in the next system.

## Neo4j Data Model

The assumption is that a system _has_ signatures: `(system)-[HAS]->(signature)`. Thus the relationship between signatures and systems are that any list of signatures are naturally linked to their respective system. 

A wormhole consists of two nodes; that of the entry signature that belongs to the system you're currently in, and the exit signature that belongs to the system on the other side of the wormhole, or the next system if you will. Since regular signatures are already linked to their respective systems, the second step is to link the wormhole entry-signature in one system to the wormhole exit-signature in the next system: `(entry)-[CONNECTS_TO]->(exit)`, and then make sure the links are timestamped, so you can filter out old links.

And that's basically it. ^^ 

## Long Term

Long-term future goal (that may never come to fruition): Add Neo4j-drivers to Node.js, write a nice web UI, and publish single-page application. A nearer goal could be to implement API calls, so that you can always see what system you're in.
