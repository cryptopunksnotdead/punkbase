# Stahlstadt.js  Talk Notes  - Inside Punkbase - SQLite (SQL.js) In Action

## What is SQLite?

<https://sqlite.org>

The world's most popular "server-less" database.  

"Server-less?!"  -  "Old School" "Server-less" - it's a library - no client/server database - 
that is,  sql queries done via "local" function calls!

Source code in C.  Public domain (that is, no rights reserved).





## What is SQL.js?

<https://sql.js.org>

SQLite compiled to JavaScript that runs - yes - in your browser (web page) "server-less"!  

Source code in C compiled via Emscripten (to WebAssembly, really ;-).

Two Parts:

- "Booter/Init/Loader" Script in "Plain" Javascript  e.g <https://cdnjs.cloudflare.com/ajax/libs/sql.js/1.6.1/sql-wasm.js> about ~100k.
- WebAssembly "Blob"  e.g. <https://cdnjs.cloudflare.com/ajax/libs/sql.js/1.6.1/sql-wasm.wasm> about ~1MB.


## What is punkbase.db?

Single-File SQLite Database, that is, punkbase.db - about ~5MB

with 10 000 records of the punk pixel art collection
with all metadata (e.g. base type, skin tone, gender, head, eyes, etc.)


## What is punkbase?

Query punkbase.db with SQL online using "server-less" web page 
thanks to SQL.js

Demo <https://cryptopunksnotdead.github.io/punkbase/>



## What is punkbase.db?  Continued

The "artbase.db" database schema:

```sql
CREATE TABLE metadata (
    -- general
    id         INTEGER      PRIMARY KEY AUTOINCREMENT
                            NOT NULL,
    base       VARCHAR      NOT NULL,
    gender     VARCHAR      NOT NULL,
    skin_tone  VARCHAR,
    count      INTEGER      NOT NULL,
    -- attributes
    blemishes  VARCHAR,
    head       VARCHAR,
    beard      VARCHAR,
    eyes       VARCHAR,
    nose       VARCHAR,
    mouth      VARCHAR,
    mouth_prop VARCHAR,
    ears       VARCHAR,
    neck       VARCHAR,
    
    -- image
    image      VARCHAR      NOT NULL
);
```

Yes, it's just a single table.


What about the pixel artwork / images? 

The images are stored "inline" 
in the image column in 24×24 px in the PNG (Portable Network Graphics) 
format with transparent background and base64-encoded
and starting with `image:data`. Example - punk no. 0:


```
data:image/png;base64,
iVBORw0KGgoAAAANSUhEUgAAABgAAAAYBAMAAAASWSDLAAAAFVBMVEUAAAAA
AABQfDNdi0NfHQmui2H/9o4qIUCBAAAAB3RSTlMA////////pX+m+wAAAHhJ
REFUeJxjYkACTORy2NLSEmAcNiCLDUVZApQDoj+wwWQ+MPz/D1f2/8MHmGlA
Bf8RRv//e4HhLEKZAMNHGIeRRYHBCdU5CXDOAZgBCQwCDA5gQ4GcWQyM/98z
/poFUTZrPaPg7wVwAw4w7EeYZrPnA4LD8h/T2wA0qh2r1DURDgAAAABJRU5E
rkJggg==
```



## What is SQL.js? Continued  - Usage - Inside Punkbase


artbase.js:

``` js
class Artbase {

  async init( database = "artbase.db" ) {

    console.log( "fetching sql.js..." );
    await loadScript( 'https://cdnjs.cloudflare.com/ajax/libs/sql.js/1.6.1/sql-wasm.js' );
    console.log( "done fetching sql.js" );

    const sqlPromise = initSqlJs({
      locateFile: file => "https://cdnjs.cloudflare.com/ajax/libs/sql.js/1.6.1/sql-wasm.wasm"
    });

    const dataPromise = fetch( database ).then(res => res.arrayBuffer());
    const [SQL, buf] = await Promise.all([sqlPromise, dataPromise])
    this.db = new SQL.Database(new Uint8Array(buf));
  }
  
  // and "server-less" function call for sql queries via exec(ute)
   query( sql ) {
      return this.db.exec( sql );
   }
}
```

That's it.


Usage

```js
const artbase = new Artbase();
const result = artbase.query( `select *
                               from   metadata
                               where  gender    = "f" AND
                               head      = "Wild Blonde" AND
                               skin_tone = "Light" AND
                               blemishes = "Mole"` );
//=>  3 punkettes ("marilyns")
```


  

## What is SQL.js? Continued  - Usage - Inside Punkbase  - "No-Code" SQL Queries

<https://github.com/pixelartexchange/artbase.js/blob/master/artbase.js>



## More Examples

[**8-Bitbase**](8bitbase) (8888 max.) - query 8bit metadata & images (24×24px) via sql & more - download all-in-one single-file sqlite database  (~4Mb)

[**Goblinbase**](goblinbase) (4444 max.)  - query goblin town metadata & images (48×48px) via sql & more - download all-in-one single-file sqlite database (~4MB)


[**Moonbirdbase**](moonbirdbase) (10000 max.)  - query moonbird (pixel owl) metadata & images (42×42px) via sql & more - download  all-in-one single-file sqlite database (~9MB)


[**Pudgybase**](pudgybase) (5000 max.) - query pudgy (penguin) metadata & images (28×28px) via sql & more - download all-in-one single-file sqlite database (~3MB)

[**Pudgypunkbase**](pudgypunkbase) (8888 max.) - query pudgy (penguin) punk metadata & images (24×24px) via sql & more - download all-in-one single-file sqlite database (~5MB)

[**Unemployablebase**](unemployablebase) (5000 max.) - query unemployable metadata & images (24×24px) via sql & more - download all-in-one single-file sqlite database  (~2MB)


and more



## Questions? Comments?
