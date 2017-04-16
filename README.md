# wormholeCypher
A small HTML5 app that makes Cypher commands for Neo4j out of pasted text, copied from the EVE Online probe scanner and bookmarks.

The Cypher commands can be dropped into the Neo4j, the grap database, so you can get an overview of your journey in and out of wormhole space.

## App Installation

The actuall (unfinished) app, a simple HTML5 file containing just CSS, HTML and JavaScript (and some additional notes), is in the  `bin/` folder.

No installation is necessary. Just download the file and open it in your favourite web browser to try it out. Feel free to fork the code.

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
