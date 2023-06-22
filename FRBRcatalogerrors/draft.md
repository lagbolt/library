## Catalog errors in modern discovery layers

I'm interested in how patrons interact with the public library OPAC.  In this note, I'm going to focus on catalog data, specifically how the extra functionality of modern discovery layers magnifies the effect of poor catalog data. 

I'll discuss four discovery layers:
  - Aspen Discovery
  - Vega Discover
  - BiblioCommons
  - CARL•Connect Discovery

I'll start off with an introduction discussing some general concepts before I introduce examples from each of the systems.

### Introduction

The four systems are not all alike.  Vega Discover is the most different, heavy on thumbnails (e.g., cover images) rather than text, and displaying subject headings as "topics" and "concepts".  CARL•Connect Discovery is the most conventional, based solidly on MARC records.  What these four systems have in common is that they can roll individual items in different formats into a single title entity.  That is, the catalog has been "FRBR-ized".  We'll see that this particular feature can result in some problems.

All four discovery layers also pull in "catalog enhancements" from external sources:
          BiblioCommons -- Novelist
          Aspen -- Novelist and Syndetics Unbound
          Vega -- Syndetics Unbound
          CARL•Connect -- Syndetics Unbound
I'll discuss this further below.

#### Clickable fields

Suppose we're looking at the item page for a book by Robert Wilson.  There are several Robert Wilsons (which is why I'm using him as an example).  Let's assume we're looking at a book by "Wilson, Robert, 1957-".  The page includes a clickable field for "Robert Wilson".  But what does the link do?  What do we *want* the link to do?

When a patron clicks on this clickable field, we don't actually know whether they're looking for books by *this* Robert Wilson or by *any* Robert Wilson, but this sort of UI/UX question is way out of scope for this note.  We'll (always) assume the narrower interpretation.

In some systems, the link might perform an author search for "Wilson, Robert", in some an author search for "Wilson, Robert, 1957-".  In **some** newer systems, the link might link to the specific author who wrote the book we are looking at.  The link might look something like:

     mylib.myils.com/author/750347935782

where the number is an identifier, internal to the system, for a particular author.

#### Series information

Series information can come from the MARC record but also from a "catalog enhancement" vendor like Syndetics Unbound or Novelist.  In Aspen Discovery, the catalog includes information from *both* Syndetics Unbound and Novelist.

Series information can be included in the MARC record in the MARC 490 field (transcribed) and the MARC 80X-83X fields (controlled).  Because one field is transcribed and the other controlled, it's possible for the MARC record to include two different series names.

So, when we look at the catalog page for a particular item, we might see series information from multiple places in multiple MARC records as well as multiple external data sources.

#### Catalog Enhancements

As I mentioned above, all four discovery layers pull in data from external sources.  In fact, if you click on ﻿"See all related resources" in Vega, the browser collects data from all of the following domains in addition to the catalog:

    iivega.com
    syndetics.com
    librarything.com

including multiple subdomains such as unbound.syndetics.com, as well as fonts from google and tracking from pendo.io.






## Examples =============

### Failure to FRBR

It's not easy to see how FRBR compliance can be extracted from MARC records.  Thus, with correct MARC records, a library can end up with this:

<LVCCLD many untamed shrews.png>

which is not helping the (public library) patron one bit.  Even someone who cares about the exact text — a student or actor, for example — is forced to click through to each item in turn to find the particular edition they're looking for.

The problem is that there's a difference between the bibliographic model that the catalog is based on, and the model that would best serve the (public library) patron.  Patrons have an internalized model that maps roughly to W-E-M-I, but with different boundaries.  For patrons for example, different editions of the same work in the same format probably count as the same manifestation.

FRBR-ized catalogs don't follow either model.  They have a three-level model (like BIBFRAME!) that usually groups "books" (books, large print, ebooks and audiobooks) into a "work" but treats movies separately.  That's not unreasonable from a patron perspective, but as we saw, it lacks a patron-friendly way of handling multiple editions of the same book.

#### Series Information

FRBR-ized catalogs typically have two kinds of pages:  one for individual items, and one for the "work" as a whole.  On the item page, series information is obviously going to come directly from the MARC record, as it does on any catalog.  The work page, on the other hand, has the challenge of combining and selecting information from the multiple records of the different items that make up the work.

CARL•Connect is unlike the other discovery layers in relying entirely on MARC item records.  When CARL•Connect builds a "work" out of a set of bibliographic records, it simply selects one of the records (nominally the most reliable) to represent the work.  Thus, when the work is displayed, the information displayed (author, title, etc.) is from that record.  CARL•Connect does not display series information on the work page.

For the three other catalogs, the display of series information depends on *how* information on a "work" is generated.  We can see from this screenshot:

<Montgomery County Series info from multiple formats.png>

that Aspen Discover is rolling up series information from all the item MARC records.  There are a few different problems that are interacting to produce this odd-looking result.  The MARC record makes no distinction between series information about the work, and series information from the publisher (like "Audible Studios on BrillianceAudio").  Similarly, there is no distinction between information about the work and information about the expression.  With no help in the MARC records to determine which is which, the discovery layer has no alternative to using everything.

The other problem is that series information can be slightly different in the records for different formats.  That's how we get this:

<Montgomery County multiple series names on grouped work.png>

This screenshot is the first item returned when doing a series search for "Sophie Kimball mysteries".  Above the first item you can see the result of rolling up different spellings of the author's name from all the results.

You can see the same issue in Vega:

<Washington County audio series info on book.png>

#### Enhanced Series Information

As I mentioned above, some systems get series information from Novelist and some from Syndetics Unbound.  This doesn't have anything to do with the fact that the catalog is FRBR-ized, but it's worth mentioning anyway.

Unfortunately, series information from Novelist is not very accurate.  Here's the Lock In series by John Scalzi:

<Montgomery County unreliable Novelist data + no indication of not held.png>

The series order is wrong ("Unlocked" is a prequel and should be first) and there's no indication whether the library actually holds the items or not.

Aspen Discovery is complicated, since it gets series data from both Novelist and Syndetics Unbound.  For the Lock In series, it displays incorrect information from Novelist, and correct information from Syndetics Unbound.  Unfortunately, the former is always displayed, and the latter is a click away.

There's also the question of what to do with a series that only contains one item.  Here is BiblioCommons trying to show series information for Notorious Sorcerer by Davinia Evans:

<LVCCLD Notorious Sorcerer - series info.png>

Technically, that's correct:  there aren't any other titles in the series.

