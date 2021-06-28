### A Cookbook of Catalog Errors

This is a set of recipes for finding errors in library catalogs.

In this note, I use examples from [Calgary Public Library](https://calgarylibrary.ca/) because they sort of asked.  You can't, and you shouldn't, infer anything from these examples about the catalog or the library.

Because Calgary Public Library uses BiblioCommons, where I give search examples, I use the syntax from BiblioCommons, either for the search box or advanced search.

License:   [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)

The short URL for this page is https://git.io/JcksP

Graeme Williams  
Las Vegas, NV  
carryonwilliams@gmail.com  
[github.com/lagbolt](https://github.com/lagbolt)

#### How many errors do you have?

I only know of one way to estimate the number of errors in your catalog:  take a sample of catalog records and check them -- by hand, if necessary.

I've done this with a random sample of 100 records from the [Las Vegas Clark County Library District](https://lvccld.org) catalog.  I used a number of tools to check the records, including Python and SQL.  The most common error was missing series information.  The best source of series information I have found is [Goodreads](https://www.goodreads.com/), which you can access either on the web or via its API.

Your error rate is useful because the tools and techniques you use will be different for different rates and total numbers.  If you have 1,000 errors, a technique which generates a set of 100 records, of which 50 are actually in error, is useful because it will resolve a useful percentage of your errors.  On the other hand, if you have 10,000 errors in the catalog, finding 50 at a time will never end.

[I have an article in Technicalities with more details.]

#### Spot Checks

- A check on authority control using an author search on "Scalzi, John"

Specifically "au:Scalzi -au:1969", which gives the items which specify "Scalzi" as the author but do not use the authorized form, "Scalzi, John, 1969-".  This returns 12 items, of which 9 are incorrect.  (The remaining three mention Scalzi in uncontrolled fields.)

Below, I discuss a Python solution for finding these cases automatically.

- A check on authority control using an  author search on "Schwab, V. E."

Some of the items returned have the author given as "Schwab, V. E." and some have "Schwab, Victoria".  LC revised the LCNAF entry in 2020 and now the correct form is "Schwab, Victoria".

You can only fix these problems by checking against the LCNAF, and by keeping up-to-date with all updates.  I'm working on a Python solution but the LCNAF is a 40GB beast.

- A check on authority control:  P!nk not Pink

The correct form -- for controlled fields -- is P!nk.  Transcribed fields will vary with the item.  You might look to the OPAC to see if these two terms can be set up as synonyms.  When someone changes their name -- and the LC revises their entry in the LCNAF -- you need to update your records.

- Deadnaming

Calgary PL is still deadnaming Elliot Page.

- Typos in subject headings

Typos in subject headings are amusing but quite rare.  Calgary PL has one instance of "Untied States" -- definitely my favorite typo -- four instances of "supsense", fourteen of "ficton" and twenty nine of "ficiton".

You can check for these by comparing subject headings to the Library of Congress data, or even just to a word list such as /usr/dict.  There are also "typo lists" available on the internet.

- A check on language data using an author search on Gabriel Garcia Marquez

Calgary PL has ~20 works by Gabriel Garcia Marquez, some of which I checked by hand.

These titles have no 041 or 546 field:  "De l'amour et autres demons"; "Love in the Time of Cholera"; and "News of a Kidnapping", at which point I stopped checking.

"Torrijos" appears to have a badly formatted 041 -- but this doesn't appear to affect searching.

###### What's going on?

I collect examples.  But I'm not scanning every record in the catalog; I'm making good guesses.  I read a lot of Science Fiction and Fantasy, so I'm familiar with the collection.   John Scalzi is a good author to check because he has written a moderate number of books in several series.  This pushes up the likelihood that authority control will fail for some of his works.

You can't infer much of anything from these spot checks.  They're like the temperature check you get at the doctor's office:  it won't tell you which COVID variant you have, or even if you're infected with a virus or a bacterium.

#### Using the OPAC search facets

This depends on exactly how your OPAC presents search results!  BiblioCommons includes a set of "filter" facets on the left-hand side.  The *intention* of these facets is to allow patrons to limit search results, but since the facets are populated with values from the catalog, a side-effect of displaying the facets is to show you data from the catalog.  To set this up, you just need to do a search which returns all the items in the catalog, such as "onorder:FALSE".  One example will suffice ...

- Published Date

If we do the "onorder:FALSE" search on the Calgary PL catalog, open up the "Published Date" facet and click on "Show more" we'll see a list of possible dates ranging from 2021 (745 items so far) to 1749 (documents from the British Government on two microfiches).  The data looks clean!  No dates like 20101102 or 1111.  Huzzah!

Let's be clear what the OPAC just did:  it went through the entire catalog and showed us the value of publication data in every record.  It doesn't mean that that every date is correct, and it doesn't mean that every record has a publication date, but it means that there are no crazy values.  Again, huzzah!

- Format

Opening up the "Format" facet, there are a couple of values worth looking at.

There is exactly one item with Format=Paperback.  It's "The Paperback Princess" by Robert N. Munsch.  I find it unlikely that the library owns exactly one paperback.

There are four items with Format=Unknown, including a French DVD, a book of John Grisham short stories, an OECD document on identity theft, and the Youth Guide to the Canadian Charter of Rights and Freedoms.

- Language

This data looks pretty clean, except that 7,612 items are classified as Language=Undetermined.  Taking a look, most of them seem to be in English, but even on the first page, there are a couple of items in First Nations languages.  I'll talk more about First Nations material below.

Also, 1,080 items are classified as "No linguistic content".  This refers to things such as classical music or tools that simply don't have any words.  Looking at the list of items, most but not all of these items are classified correctly.  It's a bit daunting to consider scanning through more than 1,000 music CDs to check if they're really purely instrumental.  On the other hand, there's exactly one audiobook, and it's misclassified.

- What else?

There's a lot more data hiding in the left-hand facets.  Keep looking!

#### Event-based Cataloging

If you're celebrating Citrus Week with a kids drawing competition, politicians photographed in front of the library holding a lemon, and a giant piñata in the parking lot in the shape of an orange, it doesn't make any sense to ignore the catalog.  And a carefully curated list of books and movies about limes and limeys is easy to tweet, but it violates the precept about "Give a person a fish ...".

Cataloging can participate in Citrus Week in two ways.  The first is with a bit of training.  You could point out, for example, that books about individual fruits will be classified under the specific fruit, while only books about citrus fruits as a whole will be classified under "citrus".  The second way is to give some sample searches.  If you show people a search for "orange OR lemon OR lime" that will demonstrate a bit of search syntax that they might not be familiar with.

The point isn't that citrus cataloging should be perfunctory the rest of the year, but rather if the event is worth a piñata, it's also worth some extra cataloging effort.

And now for some slightly more sensible examples ...

###### Indigenous History Month

At the time of writing, it's Indigenous History Month, announced on the home page of the Calgary Public Library, which links to a page of resources, with exactly zero references to the catalog.

A keyword search for "indigenous history" returns 1,168 items.  An advanced search on "anywhere:(indigenous history)" returns 1,466 items, of which 981 match a subject heading search.  That means that potentially hundreds of items are missing from a subject heading search.

What's the best way of helping patrons who are interested in Indigenous History Month?  It's an open question.  The best way to help might be to enhance catalog records so that they match a subject heading search, or it might be to educate patrons by showing different kinds of searches.  Or both.

##### First Nations

One challenge for First Nation material is getting the language coding  and description right.  In the case of Calgary Public Library, this is complicated by the fact that the MARC 546 field -- language note -- is not displayed by the OPAC, although it's possible it's included in search.

###### Nakoda

For Nakoda language materials, another wrinkle is that the LC doesn't have a language code for Nakoda.  In the Calgary catalog, one Nakoda item is coded Dakota, which looks right.

If you do a keyword search on Nakoda, you'll get 38 items, of which 22 have Language=Undetermined.  Most of these should be coded Nakoda (i.e., Dakota) or bilingual.  Many should also have a subject heading for bilingual materials.

###### Cree

If you do a keyword search on Cree, you'll get 696 items, of which 38 have Language=Undetermined.  At least half of these are Cree or bilingual.

###### Sioux

If you do a keyword search on Sioux, you'll get 50 items, of which 25 are non-fiction, 17 are fiction, and 8 are undetermined.  I'm pretty sure that these 8 items can be classified as either fiction or non-fiction.

If you look at the Regions facet, the values vary from as general as "North America" to as specific as "Fort Yates".  One is "Great Plains." and another is "Great plains".  Some cleanup is required.

###### Rinse and Repeat

I picked these three examples more or less at random.  You can go through this exercise with every indigenous group and as many search types and facets as you can.

##### LGBTQIA+

One of the things I'm interested in is the relationship between cataloger-assigned subject headings and patron-assigned tags.  BiblioCommons combines tags from patrons of every BiblioCommons library, so although at a particular library you only see the holdings for that library, the tags for each item will also come from other libraries.

One intriguing possibility for catalog enhancement is to "promote" tags to subject headings.  While it's not clear that this scheme is feasible, it's interesting to look at how much tags and subject headings overlap.

###### Bisexual

I picked this term as a test because of its putative unambiguity compared with other terms, such as "queer".  I have summary data (i.e., counts) from 100+ libraries for subject heading and tag searches for "bisexual".

At Calgary Public Library, a keyword search returned 125 items, a subject heading search returned 111 and a tag search returned 300.  An advanced search including items with the tag and excluding items with the subject heading returned 277.  So, the overlap between tags and subject headings is 23 items.  This is low but typical.

It means that there are potentially 277 tagged items that could be given a subject heading of "bisexual", more than tripling the the number of items returned by a subject heading search.  Unfortunately, I don't know of any way to check these 277 items other than one by one, by hand.

###### Lesbian

A search for subject heading="lesbian" returned 892 items; a search for tag="lesbian" returned 452 items, with an overlap of 130.  This is a lower percentage of items without the subject heading than "bisexual", but we're still talking about hundreds of items that are potentially lost to a subject heading search.

###### Queer

A search for subject heading="queer" returned 13 items; a search for tag="queer" returned 256 items, with an overlap of exactly one item.  A keyword search returned 135 items.

I'm not sure I know exactly what "queer" means, so I'm pretty sure that if I had to check the 255 tagged items to see if the subject heading should be added, I wouldn't know what to do.

###### Where's the light at the end of the tunnel?

Where the tunnel?  Three things would help to figure out what kind of catalog enhancement might be useful for LGBTIA+ material:

1. Going through at least some of the tagged items to see if the subject heading should be added;
2. Looking at search logs to see how often each type of search is used with LGBTIA+ search terms;
3. Talking to LGBTIA+ patrons specifically about how they use the catalog.

#### Automated Checks Using MARC Records

I don't have access to MARC records from Calgary Public Library, and at the time of writing, I don't have the time to scrape and analyze them.  What follows is some tests and checks I have run on other datasets using Python and SQL.  In some cases, the Python code is available.

Remember that these checks are meant to just act  as a sieve, and return a set of records that justify further checking, possibly by hand.

###### Normal Stuff

You probably already have tools for checking normal stuff, like a record with no 6xx fields, or a 6xx field with second indicator = 7 but no $2 subfield.

###### A useful summary report

I scrape MARC records into a database with one database record per MARC field.  One report I found very useful in looking for errors was to count every *combination* of MARC tag and indicator value.  In a large dataset, anomalies will appear as low counts.

###### Short Records

One simple check is just to check the number of fields in a record.  A record with less than, say, 10 fields is probably a vendor record that somehow missed enhancement.

###### 505 Contents Field

The "Basic" 505 field is theoretically acceptable, but unhelpful in practice.  The OPAC can index the title fields of the  Enhanced 505 Field, and in the case of multi-author anthologies, index the authors as well.

It's straightforward to distinguish between the two types -- without relying on the second indicator -- and list the records that include a Basic 505 field.

It's also useful to list the items with 505 records that have "partial contents" (first indicator=2) to consider if they should be enhanced.

###### Language Coding

Language coding includes the language code in the 008 field as well as 041 and 546 fields if present.  My opinion is that the 041 and 546 work in tandem.  The 041 can be used for searches, while the 546 explains the same information in plain English.

One wrinkle in checking language coding from the OPAC is that while BiblioCommons advanced search will let you search for a particular language or combination of languages (e.g., "language:eng AND language:spa"), the search engine does not appear to distinguish between subfield codes in the 041 field (e.g., $aeng$hspa vs. $aeng$aspa).  This means that some searches are better done in MARC.

There are a couple of thing to check in a record's language coding:

- simple consistency checks: for example, the language specified in the 008 should be included in the 041; or if the first indicator is "1", the 041 should include a $h subfield;
- retrieve a specific set of records (for example, keyword="bilingual" or subject="bilingual") and check that the records include 041 and 546 fields;
- check for 041 fields in "old" format.  While "$aengfrespajpnperitaaraporrus" is technically correct -- and the OPAC handles it correctly -- it's not the easiest thing to read.

[I've given a presentation to ALA CORE on language coding, and more data from the Las Vegas Clark County Library District catalog is available.]

###### Missing series information

My data suggests that Goodreads is a good enough source for series information.  If you have a Goodreads API key (or you borrow mine), you can call the API with author name and title and retrieve series information, if any.

This will work best -- checking the author and title in every record against Goodreads -- if the records are limited to a specific genre where series are common, such as Science Fiction and Fantasy, or Crime/Detective/Mysteries.

Note that enhancing records in this way -- by adding series information from an external source -- violates current cataloging rules, since the 490 field is transcribed from the item in hand.

[I've given a presentation to ALA CORE on filling in missing series information, including data from the Las Vegas Clark County Library District catalog.]

###### Duplicate Name Authority Records

It's straightforward in Python to:

1. extract contributor names from the 100s and 700s in each record;
2. sort the names;
3. check to see if consecutive entries are a name without a date followed by the same name with a date (e.g., Smith, Bob versus Smith, Bob, 1967-). 

This process will generate some false positives, so hand-checking is required, but in a public library most of the pairs you find will be errors.  I suggest that false positives will be lower if the dataset is limited to a single genre, reasoning that while there might be two authors with the same name, that's less likely within a single genre.

It's also possible to do this by hand in OPACs that display data from the Name Authority File when a patron does an author search, but BiblioCommons does not do this.



#### <div align="center">APPENDIX</div>



Miscellaneous errors I found by hand-checking records in the Calgary Public Library catalog.

```
797399095   "Cree" is not an LC subject heading
1309960095  "Nakoda" is not an LC subject heading
1040615095  041 and 500 don't look consistent
1405912095  Record is highly abbreviated
411802095   Half the authors are left off a partial 505?!
1091577095  No 6XX fields at all
729616095   Probably 008 and 041 both wrong
83291095    041 probably should be $aeng$bspa$hspa

041 is incorrect:
1143922095
1268036095
1106533095
852861095
1256075095
```



























