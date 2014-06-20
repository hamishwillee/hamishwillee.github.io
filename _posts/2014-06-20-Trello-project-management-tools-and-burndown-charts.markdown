---
layout: post
title:  "Trello project management tools and burndown charts"
#date:   2014-06-06 20:55:32
author: Hamish Willee
description: An overview of tools for making Trello more useful for Agile (and other) project management, focussing on "Plus for Trello".
tags:
- draft
---

This post summarises my *superficial* recent exploration of tools that can make Trello more useful for project management. A more accurate title might be "Why [Plus for Trello](#plus-for-trello) is *awesome by design*" :-)

# Introduction 

A friend recently suggested we use [Trello](https://trello.com/) to share our learning and work tasks. For those who are not familiar with *Trello* , it is a web-based organisational tool that is intended to help users "Organize anything, together". 

This sounded like a great idea: we'd encourage each other as we worked through the tasks, while at the same time learning more about what has become a popular tool in the Agile/Scrum community. 

After a few weeks I concluded *Trello* makes a great "to-do list", but I couldn't see why it is so popular as a *project management tool*. Project managers need to be able to track actual effort against planned effort, but *Trello*  doesn't support these concepts. As a result, there was also no mechanism for getting burn-down charts or for exporting detailed information about time spent (which I find useful for billing).

This post looks at the main options I found for adding time-tracking and burndown charts to *Trello*, especially my preferred tool: [Plus for Trello](#plus-for-trello). It also provides a few links to "top tips" for using *Trello* in an Agile project management environment.


# What is Trello?

*Trello* is a web-based organisational tool, consisting of *boards*, containing *lists* of *cards* (cards have a title, description, due date, members, labels, checklists and comments/attachments). The cards and lists can be used to represent anything, but when you're organising a project, it makes sense for the cards to be tasks and the lists to represent states: Sprint Backlog, Development, Testing, Bug, Blocked, Done, etc). You can create boards, add cards, and move them to different lists. When you're done, you can archive or delete cards, and even boards.

*Trello* gives you all this "out of the box" in the free version, along with quite a comprehensive API which you can use to query all aspects of boards, lists, cards and members. It does not give you the abiliy to export a board to CSV or similar, but since you can export to JSON (or query the information using the API) getting a human-usable form to manipulate is easy. If you upgrade to the (very reasonably priced [Trello Business Class](https://trello.com/business-class)) version you can export to CSV, and there are lots of other useful options primarily designed to make it easy to share boards within an organisation.

There is nothing inside *Trello* to help you plan or track your project effort, and there is no indicated that the *Trello* [backlog item for this functionality](https://trello.com/c/9tX8CRNm/1054-time-tracking) will be implemented (follow the link to find other useful time tracking tools). 

**Note:** There are a lot of Chrome and Firefox extensions which do "useful things with *Trello*" - like export card data. I've only checked out a few.


# Trello and Agile - a few top tips

The two blogs below provide a few "top tips" for managing your Agile project using *Trello*:

* [10 Tips for using Trello as an effective Agile Scrum Project management Tool](http://www.tommasonervegna.com/blog/2014/1/9/10-effective-tips-for-using-trello-as-an-agile-scrum-project-management-tool)
* [Five Tips for Using Trello for Scrum](http://www.civicactions.com/blog/2012/oct/10/five_tips_for_using_trello_for_scrum)

While some tips are arguable, both blogs contain a lot of "common sense". They are **well worth** the 5 minutes you'll invest reading them. 


# Plus for Trello 

 
[Plus for Trello](https://chrome.google.com/webstore/detail/plus-for-trello/gjjpophepkbhejnglcmkdnncmaanojkf?hl=en) is *Chrome-only* browser extension for tracking time spent by card, list, board and user. It is also free, open source, well supported. It is the best tool I have found (so far) for supporting time estimation and tracking on *Trello*.

The extension adds card fields in which users can enter the amount of time they have just spent on the task, a re-estimate of how much more/less time will be required (than previously estimated), and/or a comment. Once entered, the new values are automatically added to the total times in the card title (in <a href="#scrum-for-trello">Scrum for Trello</a> format).

Users can generate filtered historical reports of any of these transactions, and even group/pivot the results - for example to give all the time spent by a particular user in a particular week.

The solution allows you to view a burndown chart of the raw data points entered, view cards that are still "in progress", and drill down into the effort spent by each team member.

### The Good

The really good things about this solution are that every change/record is recorded in a google drive spreadsheet (which can be shared with a team), and that the reporting function is so flexible. This compares well with other tools, in which the data is hidden, and in any case does not include information about who made the changes, and what exactly was done (a comment).

Reports can be created from the data to get both very high and very low levels of detail on how time was planned and used. If the inbuilt reports or charts are not sufficient, then the data can be exported and manipulated in Google drive or Excel. For billing, I can dump a report of exactly how I spent my time, and group it by day, week, or card.

Other things I like about this tool:

* The context-sensitive documentation is not brilliantly written but it is fairly comprehensive, and has links to more detail in blogs - like this one on [reports](http://plusfortrello.blogspot.com.au/2014_04_01_archive.html).
* The tool is evolving fast. There are some interesting [Blogs](http://plusfortrello.blogspot.com.au/) and a [Plus for Trello Google Group](https://plus.google.com/109669748550259696558/posts) to keep users up to date.  
* The tool author is very responsive to questions
* There is good documentation on how to migrate if you've used other systems
* Lots more - check out the release notes when you download the plugin.


### The Bad (or to be precise, confusing)

Typically I've used the approach where a card is considered "finished" when it is moved to the "Done" list, at which point the team can compare the consumed time to the original estimate and learn something about our estimating ability. In *Plus for Trello* a card is considered "Done" when the remaining time is zero, so if you finish the work for a card, you should then change the estimate so that the remaining time is zero. 

The approach was very hard for me to get my head around - it feels like I'm losing my original estimates. The author (Zig Mandel) suggests that I am looking at it wrong - the estimate "E" is not the original estimate, it is the *current estimate*, and subject to change. The next version (3) of the plugin should make it possible to get reports showing the difference between time spent and the first estimate: that will solve my problem.

If you've used other tools, you may well be used to changing the esimated/used time in the card title field. This is a habit to lose - *Plus* does this for you based on the values you enter in the card. If you're migrating to *Plus* I suggest you remove any values from the card title and re-enter them using the Plus entry box.


### The Ugly

The version I am using is graphically a little shabby, and has some usability issues. Persevere!

When I first installed the plugin it wasn't clear to me how to enter my time spent on a card. I could see S and E labels, a comment field, and a submit button. I looked at the documentation and it looked like I entered the S (submitted/used time) and the E (estimated time) and the comment using a syntax like:  "*S*/*E* my comment" (where S, E are real numbers). The problem was that whatever syntax I entered into the comment field the time recorded was zero. 

The problem turned out to be that the "S" and "E" labels are actually fields for entering the values. Yes, perhaps I'm a bit thick, but when I see a solid bordered box with a filled colour and a solid-font character I think "label". I expect fields for data entry to contain character text that is italic and/or light grey in colour.

There are lots of other minor issues. For example, you access the reports and charts from the tool's hourglass icon in the Chrome taskbar. I was looking for this information in *Trello* itself in the board headings. Now the right way to do this is documented, but it would be better if the links were in the most obvious place. 

The burndown report produced by the tool is truly ugly - it is basically a graph of the stored data points. The good news is that you don't have to share this chart with your customer or management - it is simple to export the data to Excel and use its very powerful graphing functionality.

A minor point, but the reporting function does not have the ability to filter based on "Trello list". So for example, you can't list all time for cards that are "in testing". 

Lastly, I use Chrome and Firefox about equally. It would be really nice if there was a Firefox version of this extension.


# Other tools

## Scrum for Trello

[Scrum for Trello](http://scrumfortrello.com/) is a browser plugin (for Firefox, Chrome, Safari) that allows users to add time estimates and time spent directly to *Trello* cards. Estimated time is entered into the card title as a real number surrounded by round brackets, while consumed time is represented as a number surrounded by square brackets. The plugin then displays these values below the card title (and does not display them in the title). It also displays the sum of all the time estimated/consumed in each list.

The plugin itself does not provide any easy way to extract or graph the entered information, but is used by all the other tools in this post in order to do so. Note *Plus for Trello* updates the title on its users' behalf.

## Burndown for Trello

[Burndown for Trello](https://www.burndownfortrello.com/) is a tool for displaying burndown charts from your *Trello* projects. It is linked from your Trello dashboad when you install <a href="#scrum-for-trello">Scrum for Trello</a> so I presume it is produced by the same people.

The tool comes in free and paid variants (see the [Burndown for Trello Help](https://www.burndownfortrello.com/help.php) for the main differences). The free version is "more trouble than it is worth" - you have to enter the time estimated and spent in the tool's separate website and you have to go to the website to view the chart. Duplicated effort sucks!

The paid variant is much better, as the charts are displayed from within Trello using the information users enter in card titles (ins *Scrum for Trello* format). The way this appears to work is that the tool regularly (daily?) takes a snapshot of your cards and extracts the time information from the title.

While the graphs are attractive, I do not see this as flexible and well designed as *Plus for Trello*:

* There isn't any support to extract the raw data to manipulate in other ways
* The snapshot is done daily, so any no finer granularity is available
* The person who made the change in the title isn't automatically recorded, so you can't get a user-breakdown. 
* No comment is associated with each change in the label, so this can't be used to get more detailed overview of how and why the time was spent.

Despite this, if all you want is a no-effort high quality team burndown chart, the paid version offers a reasonable integration with Trello at a reasonable price.

## Custom spreadsheets and direct access to the API

*Trello* provides an API, so there is nothing to stop you writing your own web app to implement the behaviour of the other tools. 

The most common approach I've seen is to write a Google Drive spreadsheet to query the API. For example [Step by step create trello burndown](http://lsjuanny.wordpress.com/2012/08/17/step-by-step-create-trello-burndown/) provides a spreadsheet which uses a trigger to regularly get card and list data, extract the title and time information in *Scrum for Trello* format), and save the value in a row for the current data. From this data it is easy to create your own burndown charts.

This approach has the benefit that you can define exactly what information you want to get from Trello. This can be very useful, as not everything you might need is necessarily exported by any of the other tools. However as it is effectively taking a snapshot of the card's titles, it shares the same limitations as [Burndown for Trello](#burndown-for-trello) with respect to tracking individual activity.

The API does appear to [support extracting historical data](http://stackoverflow.com/questions/9812453/trello-api-determine-when-a-card-changed-lists) so a more advanced sheet/web app might get time spent/estimated data direct from *Trello* rather than by building it up by taking snapshots over time. This approach could be useful for generating a historical view of a project which was not started using any of the other tools. 


# Summary

There you have it, some good reasons why *Plus for Trello* is well worth your investigation,  why it is fundamentally better designed than its competitors, and a few links to top tips.   