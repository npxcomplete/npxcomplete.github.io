Organizational Amnesia
======================

I've recently seen [a few articles](#citations-footnote) spring up on hacker news around the problem 
of organizational knowledge retention. I thought I'd take the opportunity to 
summarize some of the better insights from the comments and add my own 2¢.

There are multiple problems we need to tackle for good retention 
of organizational information:

* Recognizing that knowledge is salient.
* Motivating actors to store that knowledge.
* Finding that knowledge when it becomes important.

Depending on the size and health of your organization you may be struggling
with different pieces of this pipeline. A ten person startup probably is 
happy with tribal knowledge sharing until they experience their first bus
ticket event. An employee leaves and suddenly the knowledge of their specialized
function is gone. 

A large and aged organization will have more problems with finding
the useful information as well as recognizing that the information they need 
is out there to be found. This results from the shear amount of information 
they've produced and continue to produce. If the information is not tightly
curated it quickly can become out of date.

The middle organization seems to have it worst of all, experiencing a mix of 
all three. A middle sized organization might not have given up on tribal knowledge
entirely while feeling like they don't, have the capacity to invest
in properly curating their knowledge base. 

The worst practice I've seen is when organizations encourage 
[blogging*](#irony-footnote) as documentation. Blogs are not always findable,
there may be many blogs that use the same key words making searching the knowledge
base difficult, and blogs are often patch work in nature. A blog entry lacks the 
needed context to understand the full message of what was attempted and why it 
got the results it did. A lesser criticism is that blogging leads devs with a more
junior attitude to focus on including dank memes than on clear communication. 

#### Community insight on the problem

It starts with those in leadership. You have to value insight.

> some folks stop innovating, they just do it "by the book". 
>
> HR quickly grasps this and hires people with less and less 
> skill, cheap personnel 'just able to apply to procedures'. 
> Other ones feel like cogs in the machine (especially the
> best ones, hunted by competitors) and quit.

> The way to prevent the nightmare of an illiterate workforce
> with only oral history is to hire people who can write and
> practice documentation-driven development.

Sometimes people don't know what to share or actively seek to hide information.

> Mandatory vacation. This is something that the finance industry has used 
> for a long time to guard against fraud -- it's hard to cover up something 
> if someone else has to do your job for two weeks straight at some point --
> but it also serves as a mechanism for requiring you to cross-train people.
> 
> Two weeks of paid vacation where the company isn't allowed to email 
> them or call them for help.

People are often short sighted and fall into the trap of tribal knowledge.

> If someone asks a question in slack, answer it via documentation,
> and send the link in slack. If people send you long answers or explanations,
> ask them to put it into the tool. When people come on board, give them access
> to the tool and see how far they get before they get stuck... then add answers
> to whatever questions stopped them.

Documentation rotts, and even fresh docs can have omissions.

> unless your company has people whose full time job it is to maintain the wiki 
> then it will always be out of date and inaccurate; just deploying some wiki 
> software tends to be pretty useless, and even in the rare cases where they 
> are maintained the medium inherently doesn't preserve the tacit knowledge 
> contained within the decision-making process itself.

If the information exists but is hard to find it doesn't exist. It won't be 
found and it won't be updated.

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

There is no signal that documentation is falling out of date.

> For something even better than a README, you could document the steps of a 
> technical procedure in a Makefile (or Fabfile) that your colleagues can run. 
> It's important to keep the scripts readable and stupid (as opposed to abstract 
> and powerful like ansible), so that people can read the steps. Some people 
> refer to this as "runnable documentation."

### Solution Space

Techniques and tools I've found are actually useful for managing 
institutional knowledge. To understand why these tools are 
valuable we need a working definiton of what constitutes good documentation.

##### Good documentation answers the critical and least often asked questions in your organization.

The least often asked questions are the ones with the most likely to be forgotten answers.
When this knowledge leaves the organization it can be very costly to regain it.

##### Good documentation answers the most often asked questions in your organization.

As the number of times a question is asked increases the wasteful cost on other employees and
by proxy the organization increases. If the answer is well documented the cost is only born by 
the person asking the question.

##### Good documentation is close to the questions it answers.

Examples:
* In software development this implies good documentation to be in-line comments and self documenting code. 
  Followed by method comments, class / file comments, and finally (my favorite) package README.md files.
* In a software UX context you might think of those little question makre icons (?) that describe the meaning 
  and purpose of a form field or button.
* In hospitals every patient's chart is hanging off thier bed.
* Your favorite / most used files are (probably) cluttering up your desktop.
* Emergency procedures checklists in airplains are immediately adjacent to the co-pilot.

In each case above when a question is asked the document that answers that question
is immediately available in the environment.

##### Good documentation is consistent

Documentation is only useful if it describes the true state of the 
world and how that world really came to be. Wrong documentation can 
be anything from an annoyance to a major hindorance. In the latter case
wrong documentation may indeed be worse than no documentation.

However, it is not enough to have documentation be consistent with the system,
it must also be consistent with other documentation.

##### Good documentation is searchable

We're all conditioned to use google. It's too late to fight that reality.

### Leveraging your "weakest" employees
One of the reasons documentation and the bus ticket problem are so salient in 
the software industry is that we have high turnover. Estimates for retention
periods vary but tend to be around 2 years, with less than ten percent of your workforce having
been around for more than 4-5 years. This implies you have a lot of people leaving...
and a lot of new hires joining your organization. 

To turn this weakness into a strength the most important thing managment can 
do is actively encourage and praise the writing and maintanance of good documentation.
When a new person joins your oganization and they won't feel immediately comfortable
merging code into a complex system. First they need to learn the system and this
will involve tripping over all The [WTFs](https://i2.wp.com/commadot.com/wp-content/uploads/2009/02/wtf.png?w=550)
in that system. Let's not lie to ourselves, that number is much higher than zero. 
So let's use their inexperience to detect and fill holes in the documentation.

Among the more comment doc files I keep in my professionally groomed repositories is a 
favorite-WTFs.md. This file describes problems and road blocks that new devs should
be made aware of and how to work around. Sometimes this describes trade-offs we see as 
the choice of least evils or that my local team have virtually no power to fix.

When a new dev starts make it clear their first *X* pull requests should be documenting
the history, reasons for, and considered alternatives of confusing parts of the code / architecture.
Help them polish the documentation and integrate it into the knowledge architecture
they still aren't familiar with and publicly acknowledge the contribution. 
NOTE: actually pair with them, don't just say to do a thing, that thing is probably ambiguous. 
Then keep this up as they submit pull requests with code & documentation enhancements.

This nurtures a culture where good documentation is recognized as valued. 
It's important how you address "bad" documentation. 
They did a good thing by creating any documentation. 
Recognize that. Tell them that. Positively reinforce the thing you want more of. 
Then help them raise it to the level that meets your standards.

If you're a new employee keep notes on the questions you ask (including the ones only spoken in your head)
AND where you go looking for answers and how quickly you found those answers or if you had to involve a new person. 
Once you're a few months in you will realize some of your searches were inefficient because 
"of course I should have thought to look <here> instead, that's where we keep <all the things>". 
 However you're in the best postion now to notice where intuition takes people in search of answers.
 Even if you think the answer should be moved maybe it is appropriate to put a link to the answer whereever 
 you first went looking.

#### Wikis
Organizations inevitably have a wiki. I consider this a bit of an anti-pattern
in software organizations because a wiki doesn't preserve locality. If the 
information isn't local someone needs to find it. If someone needs to find it
they have to know how to look for it and wiki search is pretty hit and miss.

As a software developer I have yet to find a wiki tool better than markdown, 
source comments, and git. I'll give a few props to media-wiki which is markdown-esque
and is massively better than the many unamed wikis that only permit WySIWyG editing.
I've never met a WySIWyG text editor that wasn't more pain than it was worth. Not once.

Wikis are good outside software mostly because non-technical people are used to using them.
So here's a hit list of features your wiki should have:
* Renders standard markdown and HTML. 
* Webhook or similar notification when pages change.
* History, keep every revision of a page for the last N months.
* Accepts markdown page edits by API

These features go a long way allowing third party integrations. For example,
you can efficiently integrate your own org wide search implementation or just 
replace the wikis if you decide it's below par. Not all the features you want
in a wiki need to be baked into the product. Search can be completely independent as
is the case for wikipedia and stackoverflow. Both products "have search" but 
their real search engine is google. More on this later ;)

One last side tactic for source control users that applies to wikis. 
If you're doing a good job of documenting your application in your repository
and your organization has yet to add over the top integrations such as search, 
you can automatically publish your MD files to the wiki (with appropriate backlinks)
as part of your CI pipeline. Thus your documentation lives where it is supposed to, 
and is still findable by non techinical members of your org. This is especially valuable
for operational runbooks that should live close to the alarms (which you've defined as 
configuration-as-code, right?) while also being accessible to any operator.

### Backlinking

There are a few ways you can try and solve backlinking. The simplest is to 
make a habit that when you add a link to document *A* pointed at document *B*
you also add a link on document *B* to document *A*. This also happens to be
the best approach if you can get people to do it consistently because it results 
in the backlink being put in context.

However, this is both hard to do and thankfully unnessacery. A great techincal solution is to
provide a third party indexer. In high level terms we want to answer the question
"what other documents link to this document" or even more generally 
"what information is related to this information".  Since most of our documents live online
in some form (even code) we can crawl the organization's intranet and collect these.
Your internal search probably does this already as this is the foundation of the original 
page-rank algorithm from the early days of google. With the data already in had we simply wish
to expose the source of our links. 

We can further enhance this information by adding an analytics tool on top of our first order
index. Providing a browser plugin to employees that tracks links as they are traversed and time
spent reading specific documents can help us identify dead documents and documents that are to 
highly ranked according to search. Note that some employees have 1984 levels of discomfort with 
this type of tracking so please be a good citizen and don't log which users are doing a thing.

The browser plugin can provide a search option directly in browser, as well as suggest
documents that might relate to whatever your user is currently viewing.

Better still your index can be used in pipeline to ensure cross linking
between tools do not become broken. Honestly why do more wikis not automatically 
detect broken links when they point at other documents IN THE SAME WIKI.

##### Executable documentation doesnt rot.

Coding practices I don't see often enough include Test-first development. 
A well written test tells you something about the SUT (system under test).
Better still the "documentation" is now executable. It is self verifying and 
therefore less likely to fall out of date. This is only one reason leaders
should insist on writing tests first.

Markdown provides a code snippet syntax:
```markdown
 |```bash
 |echo hello
 |```
```
A simple parsing tool can strip away all the explination leaving only the code. 
Code which can be executed as part of the CI loop. If your documenation is talking 
about an application instead of code then consider image recognition based user
interface tests. Be warned such tests are often a bit prone to false negatives 
(i.e. failing because a web page was slow to load). While such tools wont stop you 
from making causing the documentation to fall out-of-date. They will provide you a 
signal to go fix it. The rest is on you.

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
