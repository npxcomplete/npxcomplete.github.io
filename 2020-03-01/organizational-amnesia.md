Organizational Amnesia
======================

I've recently seen [a few articles](#citations-footnote) spring up on hacker news around the problem 
of organizational knowledge retention. I thought I'd take the opportunity to 
summarize some of the better insights from the comments and add my own 2¢.

There are actually multiple problems we need to tackle for good retention 
of organizational information:

* Recognizing that knowledge is salient.
* Motivating actors to store that knowledge.
* Finding that knowledge when it becomes important.

Depending on the size and health of your organization you may be struggling
with different pieces of this pipeline. A ten person startup probably is 
happy with tribal knowledge sharing until they experience their first bus
ticket event. An employee leaves and suddenly the knowledge of their specialized
function is gone. 

A large and aged organization will have more problems with not only finding
the useful information, but also recognizing that the information they need 
is out there to be found. This results from the shear amount of information 
they've produced and continue to produce. If the information is not tightly
curated it quickly can become out of date.

The middle organization seems to have it worst of all, experiencing a mix of 
all three. A middle sized organization might not have given up on tribal knowledge
but at the same time they don't, or feel they don't, have the capacity to invest
in properly curating their knowledge base. 

The worst practice I've seen is when 
organizations encourage [blogging*](#irony-footnote) as documentation. Blogs are not always findable,
there may be many blogs that use the same key words making searching the knowledge
base difficult, and blogs are often to patch work. A blog entry lacks the 
needed context to understand the full message of what was attempted and why it 
got the results it did. A lesser criticism is that blogging leads devs with a more
junior attitude to focus on including dank memes than on clear communication. 
 
Let's see what the community has to say.

### Recognizing what is Salient.

This starts with those in leadership. You have to value insight

> some folks stop innovating, they just do it "by the book". 
>
> HR quickly grasps this and hires people with less and less 
> skill, cheap personnel 'just able to apply to procedures'. 
> Other ones feel like cogs in the machine (especially the
> best ones, hunted by competitors) and quit.

> The way to prevent the nightmare of an illiterate workforce
> with only oral history is to hire people who can write and
> practice documentation-driven development.

Coding practices I don't see often enough include Test-first development. 
A well written test tells you something about the SUT (system under test).
Better still the "documentation" is now executable. It is self verifying and 
therefore less likely to fall out of date. This is only one reason leaders
should insist on writing tests first.



### Motivating Actors

> Mandatory vacation. This is something that the finance industry has used 
> for a long time to guard against fraud -- it's hard to cover up something 
> if someone else has to do your job for two weeks straight at some point --
> but it also serves as a mechanism for requiring you to cross-train people.
> 
> Two weeks of paid vacation where the company isn't allowed to email 
> them or call them for help.

This one depends on the notion that whoever is going on vacation would
otherwise be asked questions or their owned work would be picked up by 
others during that time. A situation that is not always true of developers
but is true for SREs or [DevOps†](#devops-footnote) practitioners.

> If someone asks a question in slack, answer it via documentation,
> and send the link in slack. If people send you long answers or explanations,
> ask them to put it into the tool. When people come on board, give them access
> to the tool and see how far they get before they get stuck... then add answers
> to whatever questions stopped them.

One of the reasons documentation and the bus number problem are so salient in 
the software industry is that we have high turnover. Estimates for retention
periods vary but tend to be around 2 years, with <10% of your workforce having
been around for more than 4-5 years. This means you have a lot of people leaving...
and a lot of new hires. 

We can turn this weakness into a strength. One of the big things managment can 
do is actively encourage and praise documentation of WTFs by new developers.
When that new person joins you and they aren't going to feel immediately comfortable
merging code into a complex system. First they need to learn the system and this
will involve tripping over all The [WTFs](https://i2.wp.com/commadot.com/wp-content/uploads/2009/02/wtf.png?w=550) 
in that system. Let's not lie to ourselves, that number is much higher than zero. 
So let's use their inexperience to detect and fill holes in the documentation.

When a new dev starts make it clear their first X pull requests should be documenting
the history, reasons for, and considered alternatives of confusing parts of the code / architecture.
Help them polish the documentation and integrate it into bits of the code base 
and knowledge system they may not know exist yet (actually pair with them, don't 
just say to do a thing, that thing is probably ambiguous) and publicly acknowledge 
the contribution. Then keep this up as they submit pull requests with code enhancements.

This nurtures a culture where (good) documentation is recognized as valued. You will
see "bad" documentation. It's important how you address this. They did a good thing
by creating any documentation. Recognize that. Tell them that. Positively reinforce
the thing you want more of. Then help them raise it to the level that meets your standards.

### Finding Knowledge

> unless your company has people whose full time job it is to maintain the wiki 
> then it will always be out of date and inaccurate; just deploying some wiki 
> software tends to be pretty useless, and even in the rare cases where they 
> are maintained the medium inherently doesn't preserve the tacit knowledge 
> contained within the decision-making process itself.

Organizations inevitably have a wiki. I consider this a bit of an anti-pattern
in software organizations because a wiki doesn't preserve locality. If the 
information isn't local someone needs to find it. If someone needs to find it
they have to know how to look for it and wiki search is pretty hit and miss.

> consider keeping the medium simple, and avoiding a proliferation of locations, 
> formats, a dozen bullpoop communication SaaSes, etc. For most software work, 
> for example, inline embedded source code comments and API docs can be an easy way 
> to try to keep a lot of information accessible in context and maintained. Some other 
> information that doesn't fit well in source code, such as ops architecture and 
> procedures, might be Markdown files in that same code repo, or another one. 
> The occasional video file you just can't check into git might be a rare 
> indispensible one, but can still be linked from a Markdown file that's in your 
> repo, but even then, maybe you also have a text transcript in the repo, or 
> someone turns a talk into edited docs in the repo.

I can't up-vote this one enough. I have yet to find a wiki tool better than 
markdown / comments and git.

If the documentation is inline and relevant to a single location then inline 
is enough. If a high level concept needs explaining and is relevant in multiple
locations put it in a package MD file and put a link inline in code anywhere the 
question might be asked. If you really need binary data (images / video) then
there should be a link to it AND a link from it back to the MD file.

Note: these things are now coupled. That coupling should be be part of your 
CI/CD automation. If the link is removed from documentation or the 
page / image / video is deleted from the website or wiki then there should be a 
notification sent to the component and resource owners.

> For something even better than a README, you could document the steps of a 
> technical procedure in a Makefile (or Fabfile) that your colleagues can run. 
> It's important to keep the scripts readable and stupid (as opposed to abstract 
> and powerful like ansible), so that people can read the steps. Some people 
> refer to this as "runnable documentation."

For something even better than a make file you can have a markdown file with 
examples usages that can be pulled out and executed as part of CI. 

Remember that anything you do to try and make communication a historical artifact
will quickly become noise in the signal. Just because your wiki / email / slack 
conversation is searchable doesn't mean it's useful. Without curration it will 
with age become a hindrance to finding knowledge. The challenge of expiring 
information is just as important for maintaining knowledge as documenting the 
information in the first place.

##### NPxComplete's first law of documentation

Any process knowledge that is not active enforced, or at least enabled, by 
your CI/CD or Incident Management automation will be out dated, ignored, or forgotten. 

### Fin

<a name="devops-footnote"></a>† DevOps is the act of having developers handle 
operation for the thing they develop. It is not hiring Devs into an SRE role.
If the people pushing features aren't the people on call you're not doing DevOps.

<a name="irony-footnote"></a>* The irony that I'm saying this in a blog entry is not lost on me ;) 

<a name="citations-footnote"></a>[Ask HN: How to encourage and maintain a long term organizational knowledge base?](https://news.ycombinator.com/item?id=19098926)

[Ask HN: Good ways to capture institutional knowledge?](https://news.ycombinator.com/item?id=22454333)