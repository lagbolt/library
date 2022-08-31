## Guidelines for a Patron-centered OPAC

tl;dr:  Look at patron workflows in as many different OPACs as you can.  Take the best from each one.

It's important that the OPAC support bibliographic tasks that are not directly related to the catalog.  You want a patron's bibliographic world to overlap with the library's bibliographic world, and for the OPAC to support that overlap.

This note is divided into two parts.  The second part is a list of requirements for the ideal patron-focused OPAC.  The first part is some discussion motivating the items in the second part.

License:   [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)

Graeme Williams  
Las Vegas, NV and Frederick, MD  
carryonwilliams@gmail.com  
[github.com/lagbolt](https://github.com/lagbolt)

## Part 1:  Discussion

To the extent that there is any theory behind this note, I believe that while interacting with the OPAC, the patron will be focused either:
* on their OPAC account (e.g., adding a title to their TBR list or tagging a title), or
* on the library holdings, or
* availability

The patron will be concerned with:
* a title in any format or a particular format
* a title as part of a series
* a particular branch or the whole system

The OPAC should provide the patron as much information as it can as soon as it can.  While counting how many clicks it takes to perform a given task ("click counting") might or might not be useful in evaluating an interface, the clicks in an OPAC tend to be less straightforward than in, say, a shoe store.  In an OPAC, two clicks away can feel like a long way.

Availability is more complicated for the patron than it is for the library.  For the library, holdings are just a set of not very complicated database records; for the patron, availability can be a complicated calculation depending on urgency, time, money and distance.  Borrowing books from the library isn't free; just getting to the library requires gas money or bus fare.  Under some circumstances, it will be better for the patron to get a book from Amazon or the local bookstore.

### An example

Every Friday afternoon, I'd ask my kids what homework they had to do over the weekend, and they'd assure me that they had none — until Sunday morning, when they'd reveal some project or other.  Let's suppose the topic was snails.

Certainly, I can search the library catalog for books on snails, but that only tells me what books the library *owns*, not what is available.  What I need to know is the *closest available* book on snails.

Now I don't know of an OPAC that will sort search results by closest available.  Typically, I can *limit* results to items that are available at a particular branch, so I could start with the closest branch and work out from there, but I'd have to do the work of selecting branches myself, always assuming that I have a list of branches sorted by distance.

[FCPL](https://www.fcpl.org) (which uses TLC Carl*Connect) has a nice feature that shows availability by distance, but only on the item page, so you'd have to go through the search results item by item — at a snail's pace, so to speak.  Also, this feature is limited to the mobile interface (why?).

[LVCCLD](https://lvccld.org) (which uses BiblioCommons) has a feature which is moderately helpful.  You can specify one or more "favorite" branches, and the search results page will include whether each item is available at a "favorite" branch — although not which one.

The goal of an OPAC isn't, "Respond to the patron with some information using the fewest database queries" — it's "Respond to the patron with as much useful information as possible".

#### So what?

Parsimony!  OPACs limit the amount of information they show a patron at any given time.  This helps the OPAC with raw response time — pages come back quickly — but is not so helpful with the ease or speed of task completion.

For a patron task like, "find the closest available book on snails", an OPAC can be better or worse at efficiently displaying the information the patron needs to complete their task.  That's why an OPAC should be evaluated against patron tasks, and not abstract display requirements.

### Bibliographic Models

There's something called [Naive Physics](https://en.wikipedia.org/wiki/Na%C3%AFve_physics), which is what ordinary people think about physical phenomena.  It's different than the more complicated models that actual physicists use.  Similarly, library patrons don't use a bibliographic model like FRBR, WEMI or LRM; they have internalized a "naive bibliographic model".  In this note, I'll use "title" to refer to a work which can exist in different formats, such as a book which can be a book or audiobook (etc.), and "item" to refer to a title in a specific format, such as a large print book or audiobook on CD.  Like most patrons, I won't make much of the difference between "work" and "expression".

What matters to the patron is how well the OPAC displays alternative formats in search results and lists, so that the patron can choose among them.

### Lists

Many of your library patrons will have a to-be-read list that they have collected from sources outside the library, such as Twitter, or these days I guess, BookTok (i.e., books on TikTok).  If patrons are going to use the OPAC to keep track of their TBR list and not scribble it on the back of CVS receipts, it has to be *simple* to create lists in the OPAC.

I want to take a small detour to talk about how software is designed versus how it is used (from [BiblioCommons list launch](https://www.bibliocommons.com/list-launch), copied to [a shared file on Google Drive](https://drive.google.com/file/d/1e1lDZ2dwlwUbRrJkVnOju5E2Fx5KVtbj/view?usp=sharing])).  Apparently, BiblioCommons thinks you can tell people what to do.  Here's BiblioCommons product marketing on how that worked out:

> "Lists in BiblioCommons are meant to serve one primary purpose: providing curated recommendations that are shared in the platform. ... However, our analysis of how lists were being used showed that a percentage of users were creating lists as a method to track the items they were reading or were going to read. Our users were essentially creating Lists instead of using Shelves."

Quite.  People have been opening paint cans with screwdrivers for thousands of years.  So when an OPAC vendor tells you such and such a feature is for such and such a function, take it with a grain of salt.

Here's how lists work in BiblioCommons.  It doesn't matter if BiblioCommons is better or worse than other OPACs, but it is *complicated*.  BiblioCommons wants lists to be a kind of social media where patrons follow other patrons and librarians and see when they create or update lists.  Staff lists and patron lists are implemented using the same mechanism, so they look and act the same.

In a BiblioCommons OPAC, a list can either be "draft" or "published" — or both.  If you add an item to a published list, the system will automatically create a draft for you, but everyone else (assuming the list is public) will see the older, published version.  This makes sense, but there are unfortunate limitations to "draft" lists:  you can't click through an item to see the item page, and a draft list doesn't show availability information.  To see item availability, you have to find the item again.  Also, you can't make any changes to a published list, such as adding a note to an item.  To do that, you have to manually switch the list to "draft".  In practice this means flipping a list between draft and published many times.

A limitation of lists in BiblioCommons is that you can only add items to a list, not titles.  This means that the availability information on the list page is going to be limited to one format.

On the other hand, BiblioCommons has a nice feature where you can add a web link to a list instead of a catalog item.  This neatly gets around the problem that the catalog is limited to the library's holdings.  But supposing you add an Amazon link for a to-be-published book and later the book is added to the catalog.  That makes your Amazon link something of an orphan.

At [FCPL](https://fcpl.org), staff lists are hosted on the library web site and are completely separate from the lists that patrons can create in the OPAC.  For example, [Building Bridges](https://www.fcpl.org/building-bridges-adult-titles).  This is a nicer format but it means you can't see availability information right on the list page.

You can see another nice lists feature in action at GoodReads.  Here's [a list of all the books tagged 'science fiction'](https://www.goodreads.com/genres/science-fiction).  If you hover over a title, you'll get a pop-up with a description of the title.

### Tags

Tagging is useful for any number of OPAC functions, such as allowing the library community to add non-LCSH vocabulary.  It's useful to patrons as a complement to lists.

Suppose you're *very* interested in roses.  Your public library is likely to have quite a few books on roses (FCPL has 35 items, LVCCLD has 274, NYPL has 752).  There are a few LC subject headings, including "Roses", "Rose Culture" and "Rose Gardens", but it's unlikely to be sufficient for a rose expert.  As you read all these books, you can add your own tags in as much detail as you like:  specific varieties, seasons, shade, fertilizer, color, etc, etc.  Note that you can't do this level of detail with a few lists.

Of course, tags will be used for more mundane purposes, like "tell my sister about this".  In either case, it makes sense that once you've created a tag, you should be able to find it again.

### Searching and Documentation

I mean documentation for patrons.

[FCPL](https://fcpl.org), which uses TLC's Carl*Connect, includes a query language you can type into the simple search box.  For example, "subject:frogs".  But as far as I find, there is no documentation on the query language anywhere.  Although not every patron will be interested in typing boolean queries in a strange query language, I hope we can agree that zero documentation is not quite enough.

And it's not straightforward.  The advanced search page lets you search for a tag by "starts with" or "exactly matches".  So how does "tag:frog" work in the simple search box?  It's "exactly matches".  How does "author:Smith" work in the simple search box?  It's "starts with".

This is the sort of wrinkle that makes clear that effective documentation is a must.  A typical OPAC is going to have a few different ways of searching, and the different methods and terminology won't exactly match.

## Part 2: A Laundry List for the OPAC

(My account, reading history, etc.)

Show everything related to my account on a single page (tabs are OK)

Let me decide whether to turn features on or not, such as keeping reading history, putting information in cookies, displaying my "suggest a title" suggestions, etc

Drop a cookie specifying my local branch so you know which it is without me logging in

Let me add titles to my reading history

Let me add titles to my reading history that the library doesn't own (e.g., via a link to Worldcat or Amazon)

When a book on my reading history is part of a series, add a clickable link to the next book in the series

My reading history should have some (most?) of the controls that a search results page has, such as displaying oldest first or newest first, only a particular format, etc, etc.

Display all my "suggest a title" suggestions in my account (not in a separate place in the OPAC!), including their status

Let me to choose whether or not to put a hold on a book that I submit to "suggest a title".

(Lists and Tags)

Let me create lists of books (etc.) by title or item

Let me add to a book list titles that the library doesn't own (e.g., via a Worldcat link)

When displaying a list, I should have some (most?) of the controls that a search results page does, as above.

When displaying a list, include (clickable) series information when applicable

Let me add a note to a list entry.  (Unbelievably, TLC Carl*Connect doesn't let you do this.)

Include in my account display the tags I have created

Allow both public and private lists; allow both public and private tags.  Allow me to share a private list

(Searches, search results and item pages)

Everything should be searchable from one place.  (If patrons have to search Overdrive or Libby for ebooks, and Hoopla for movies, and somewhere else for graphic novels, they might decide it's not worth the trouble.)

Show on the search results page if a book is part of a series and which book it is in the series.  (Make sure your metadata is as good as Goodreads.)

When displaying an title, either in search results or on its own page, if I have read it, indicate that

When displaying an title, either in search results or on its own page, if I have read another title in the same series, indicate that.

Handle pseudonyms in a sensible way (e.g., with a note at the top of the screen)

Don't under any circumstances show me an authority file.  E.g., if I do an author search and it matches more than one author, show all results and list the five (ten?) most popular authors at the top of the search results page with clickable links

If a search facet has more possible values than are displayed at first, the "More" button should display them all immediately (e.g., in a dialog box) and not water-drip values ten at a time.  (Carl*Connect, I'm looking at you.)

The search results page for a series search should list the titles in series order; if more than one series matches the search, a clickable link for each series should be included at the top of the page.  As above, the search results page should indicate if I have read some books in the series.

(Availability)

Show availability information on the search results page, and when displaying lists.  Do not require extra clicks except to display a complete list of availability by branch.

If I have set a local branch in my account, include specific information on availability at that branch as well as system availability.  Similarly when using an OPAC terminal inside a branch.

Summarize availability including both holdings and availability (e.g., "3 copies, 2 available")

(Hold requests)

*Note:  From my perspective as a patron, the way any OPAC handles hold requests is a few decades pre-Ramanajan.  The notes below are an attempt to drag the functionality into the second half of the 20th century*

Allow me to put a hold on the specific copy of a book from my local branch (to reduce my carbon footprint)

When I submit a hold request for a title, let me say which book formats (large print, trade, mass market, etc.) are acceptable

When I submit a hold request for a title, let me say which formats (ebook, audiobook, book book) are acceptable

Let me freeze a hold request

(Miscellaneous)

Spelling correction for searches — as good as Google

Noise word removal for searches — as good as Google

Include a (big red) button on every page labelled "Looks wrong?"

Add a link to WorldCat on the failed search page.

Tell me when other people are waiting for a book I have out.  Let me choose whether I get an email, or just an indication on my loans page.  Send the "you have a book which is due soon" email earlier if other people are waiting for the book.

(Plus two pipe-dreams ...)

Limit the number of hold requests that are satisfied at once.  For example, when two hold requests have been satisfied, automatically freeze the remainder.

Expose an web API for authenticated patrons so that we'd don't have to use your crummy web site at all yes of course with current availability information yes I know what the performance impact will be save the time of the reader