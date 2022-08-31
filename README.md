# Punkbase

query punk metadata & images via sql & more - all-in-one single-file sqlite database, that is, punkbase.db (~5MB)


Try the "serverless" query web page online

- [**cryptopunksnotdead.github.io/punkbase**](https://cryptopunksnotdead.github.io/punkbase/)


Let's try out some sql queries and let's look (and drill-down) for marilyn punkettes (w/ moles).

Click on "gender: f" in any punkette and you will filter only punkettes.
Click on "head: Wild Blonde" in any punkette and you will add a "Wild Blonde" filter
resulting in 144 punkettes.

Or try in "raw" sql:

```sql
select *
from   metadata
where  gender = "f" AND
       head   = "Wild Blonde"
```

=> 144 punkettes

Now let's drill down.  Click on "skin_tone: Light".

```sql
select *
from   metadata
where  gender    = "f" AND
       head      = "Wild Blonde" AND
       skin_tone = "Light"
```

=> 48 punkettes

And now let's drill down further. Click on "blemishes: Mole".

```sql
select *
from   metadata
where  gender    = "f" AND
       head      = "Wild Blonde" AND
       skin_tone = "Light" AND
       blemishes = "Mole"
```

=> 3 punkettes

And so on. Voila! Three super-rare marilyns. Where's the blue-eyed marilyn with hot lipstick?

Tip - yes, you can  - generate your own ultra-rare never-before-seen original, see [**Design Your Own Matt & John's® Ye Olde' Punk (Anno 2017) (24×24) Wizard »**](https://cryptopunksnotdead.github.io/pixelart.js/yeoldepunks/).



##  Run Locally ("Serverless")

Yes, you can - run locally (no database server required) - 
download or clone the punkbase git repo 
and run a local webserver to serve the static web page and sqlite database. 

In node use:

     $ npx http-server

In ruby use:

     $ ruby -run -e httpd . -p 8080

Or use your local webserver of choice.




## Inside


For now all data (10 000 records)
is in the metadata table.
The table definition reads:


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

Notes:

- id is the collection "series" no. from 0 to 9999
- base is the punk type e.g. Human, Zombie, Ape, Alien
- gender is the male / female e.g.  m / f
- skin tone is the human skin tone (1/2/3/4) e.g. Dark / Mid / Light/ Albino  - note: NULL for zombie / ape / alien
- count is the attribute count e.g. 0 / 1 / 2 / 3 / 4 / 5  - note: as number


The attributes are broken up in ten categories:

- blemishes: Rosy Cheeks, Mole, Spots
- head: Shaved Head, Peak Spike, Vampire Hair, Purple Hair,
  Mohawk, Mohawk Dark, Mohawk Thin, Wild Hair,
  Crazy Hair, Messy Hair, Frumpy Hair,
  Stringy Hair, Clown Hair Green, Straight Hair,
  Straight Hair Dark, Straight Hair Blonde,
  Blonde Short, Blonde Bob, Wild Blonde,
  Wild White Hair, Orange Side,
  Dark Hair, Pigtails, Pink With Hat,
  Half Shaved, Red Mohawk,
  Cowboy Hat, Fedora, Hoodie, Beanie,
  Top Hat, Do-rag, Police Cap,  Cap Forward,
  Cap, Knitted Cap, Bandana, Headband, Pilot Helmet,
  Tassle Hat, Tiara
- beard:  Shadow Beard, Normal Beard, Normal Beard Black,
  Big Beard, Luxurious Beard, Mustache, Goat,   Handlebars, Front Beard, Front Beard Dark,
  Chinstrap, Muttonchops
- eyes:  Small Shades, Regular Shades, Classic Shades,
  Big Shades, Nerd Glasses, Horned Rim Glasses,
  3D Glasses, VR, Eye Mask, Eye Patch,
  Welding Goggles,
  Clown Eyes Green, Clown Eyes Blue, Green Eye Shadow,
  Blue Eye Shadow, Purple Eye Shadow
- nose:  Clown Nose
- mouth:   Smile, Frown, Buck Teeth, Hot Lipstick,
  Black Lipstick, Purple Lipstick
- mouth_prop:    Cigarette, Vape, Pipe, Medical Mask
- ears:  Earring
- neck:  Silver Chain, Gold Chain, Choker



The images are stored "inline" in the image column in 24×24 px in the PNG (Portable Network Graphics) format with transparent background and base64-encoded
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

<!--
note: data:image looks to get filtered by github page ?

resulting in (if you add / paste the image data to / into the src attribute):

<img src="data:image/png;base64, iVBORw0KGgoAAAANSUhEUgAAABgAAAAYBAMAAAASWSDLAAAAFVBMVEUAAAAAAABQfDNdi0NfHQmui2H/9o4qIUCBAAAAB3RSTlMA////////pX+m+wAAAHhJREFUeJxjYkACTORy2NLSEmAcNiCLDUVZApQDoj+wwWQ+MPz/D1f2/8MHmGlABf8RRv//e4HhLEKZAMNHGIeRRYHBCdU5CXDOAZgBCQwCDA5gQ4GcWQyM/98z/poFUTZrPaPg7wVwAw4w7EeYZrPnA4LD8h/T2wA0qh2r1DURDgAAAABJRU5E">

-->


## Making-Of - Yes, You Can - Build Your Own Punkbase From Zero / Scratch

See the punkbase script in [**/punkbase**](https://github.com/cryptopunksnotdead/punks.sandbox/tree/master/punkbase) in the punk.sandbox for
the building your own database from zero / scratch.




## Questions? Comments?

Post them on the [D.I.Y. Punk (Pixel) Art reddit](https://old.reddit.com/r/DIYPunkArt). Thanks.

