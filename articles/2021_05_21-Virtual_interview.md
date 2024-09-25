# Questions you may think of asking me

**What did your entrepreneur experience give you?**

Skills to solve problems when massively under-resourced. An eye to see where people's pain really is. Practical ability to take calculated risks and having an honestly viable plan B. Ability to change and properly multitask. An understanding of the need of validating all the base assumptions constantly and adjusting the plans and execution. Time to Market is everything.

**How to best pass a message during a presentation?**

Treat your audience with respect, be honest, do your homework and come prepared. Have a deep understanding of what you are talking about. Make your point simple to digest. Bring. Them. A Real Value.

**What ideally an IT project needs to do to be successful?**

Build and maintain a product that people will willingly use, in a minimal time, with a minimal cost, solving people's pain well enough for them not to abandon it, adaptable for future changes. Overdeliver.

**OK, but how to do it?**

Find a person with a _real_ pain. Be close to your customer, understand the pain and remove it.

**Is it easier to say than to do?**

Of course it usually is. Sometimes it is an exact science, sometimes it is rather more an art.

**Do I need a good Developer for this or an Architect?**

The definitions are blurred here and the size of the project matters a lot. A good developer usually does know how to code a solution for reasonably any problem. A good architect has enough experience to know how to solve the problem in 3+ different ways and will fit the solution into your landscape. Sometimes even without coding. This experience is gained with blood and sweat, that's why solutions from non-technical architects are usually way more expensive than they could be.

**How to minimize both the TTM (Time to Market) and TCO (Total Cost of Ownership)?**

When solved blindly by adding more people these two requirements become, indeed, controversial. More people may help the delivery; but, fundamentally, "it is impossible to get a baby in one month having 9 women". Plus the communication overhead will inevitably increase.

Another option with a superlinear positive impact on a long run is to focus on minimizing the _Cost of Change_ (_CoC_). This includes both widely known things like: _increasing modularity_, _automated testing_, _continuous delivery_, as well as the less famous: _focusing on standard flexible and stable interfaces_, _choosing a language with a higher level of abstraction and a strong type system_.

**Why is choosing a language with a strong type system is a good idea?**

Strongly typed languages naturally:

- decrease the requirements for the amount of (automated) testing by disallowing incorrect scenarios during the compiling time.
- decrease the size of the codebase and amount of "belt and braces".
- bring smarter people to the project, capable of understanding more complex concepts.

Weakly typed languages (like Python or Javascript) allow you to, instead, hack something very quickly.

**Shall I just use TDD/BDD instead?**

Well … the TDD is a great idea with a lot of added value, when used reasonably. But when used unreasonably (with a lot of mocks and having a test per every single function) the codebase quickly turns into a so-called _TDC_ - "test driven concrete" - where the work on tests (which are, from a business perspective, fundamentally a waste) leaves no time for implementing business requirements. BDD/Cucumber is even worse from the CoC perspective - the hypothetical ability to show tests written with them to non-tech people has a cost of impossibility of automated refactoring of the under-bonnet Cucumber magic.

The goal behind any testing is to guarantee the correctness of the end result. A great part of it can be achieved easier by using a stronger typed language properly. And this part is the most business unrelated of low level technical unit tests. Luckily, the industry is turning this direction now.

**What languages are you talking about?**

- Javascript &#8594; Typescript (or even Blazor)
- Java &#8594; Kotlin (Scala 2.x is opionatively a bit too academic)
- in .Net is better to stick to the latest C# (but practising F# has made me personally a way better programmer)
- C/C++ &#8594; Rust.
- In Data Science this option mostly doesn't exist yet, and the most shifts are focused on drifts from Matlab and R towards Python for frameworks, tooling, and community; and to Julia for speed.

**What should be a focus while choosing a new platform or software system?**

1. Answering whether or not a candidate system does the job well enough.
2. Do we have a plan to cheaply/easily decommission it in favour of a competitor when it fails to satisfy your needs for whatever reason? This usually requires the platform to follow industry standards and have some guarantees in:
   - Communication (protocols, their versions, IDLs, etc.)
   - Deployment (these days containerization with, say, Docker and Kubernetes support gets crucial)
   - Data imports/exports

**When will Microservices solve the World hunger?**

It's a yet another blurred term and a very large topic. Both Akka actors, small REST Web apps, and fully blown (No)SQL databases in Docker and Kubernetes claim these days that they are Microservices. And that they will break your big old Monolith into nice fancy Microservices which are easier to manage (look at Netflix!).

Well… All three can, and, when applied accurately, have already changed the world of software development, by adding more (very powerful) options into the developers toolkits. Or not, by bringing you a new and shiny Distributed Monolith instead. Because distributed systems are hard. Sometimes, very hard. Mostly impossible without a lot of automation in provisioning, CI/CD, and fleet management. And have a tendency to leave you in a _ReadUncommited_ world, while correctness is the hardest thing to retrofit.

To solve Netflix's problems their way, you need, first, to have problems of their size (even their Head of Architecture once suggested - don't). Just pick the tools best suited to solving your exact problem, remember about KISS and YAGNI. And if Docker and K8s, Actors, etc, fit the bill - use them, they are great and bring a lot of value. (An opinionated suggestion - don't get stuck with REST - explore the "interface first" and "embedded streaming" options - such as gRPC, Thrift, GraphQL).

**We are building a BigData platform, what should we be aware of?**

&quot;BigData is the data that _doesn't fit into one machine_&quot; © CEO of Elastic. Before stepping into the BigData solutions space, the one-machine-not-fit assumption needs to be validated. These days even laptops and smartphones can process [billions of records per second](https://clemenswinter.com/2018/07/09/how-to-analyze-billions-of-records-per-second-on-a-single-desktop-pc/), read [100s of millions of them per sec](https://clemenswinter.com/2018/08/13/how-read-100s-of-millions-of-records-per-second-from-a-single-disk/) from an SSD, [update aggregates on 100s of millions of records streaming in milliseconds](https://materialize.com/taking-materialize-for-a-spin-on-nyc-taxi-data/) and beat [Spark clusters 200-2000x times per core](https://github.com/frankmcsherry/blog/blob/master/posts/2015-01-15.md). And these are just small, normal laptops. In Clouds, you can easily get machines with up to 6TB of memory, huge SSDs and tons of cores (yes I'm aware of that your GC may not like it).

BigData topic had suddenly disappeared from the Gartner's Hype Curve (as an already solved problem?).

BigData out-of-the-box solutions are great, but all come with their own problems and painful trade-offs. Always check and validate first if your problem cannot be solved via decomposing it into smaller, more manageable bits first.

**Should we use BigData platforms at all?**

Maybe yes, maybe no. All depends on the shape and amount of the data you have in hand. And the available hardware layout. So try to test scenarios actually relevant to your very setup, don't trust any marketing materials, collect your own numbers, have a plan to easily decommission the chosen platform in favour of a competitor for a case it stops to satisfy your needs for whatever reason.

**Reactive or Imperative?**

Imperative is always easier to reason about. Akka/Erlang Actors and Observables are way harder to follow than async/await and coroutines. Same applies to CQRS/Eventsourcing against state management.

**How to de-risk an IT project from massive unexpected delays?**

By having a plan of action and validating this plan against reality in control points, adjusting either the plan or the scope. It doesn't mean following Waterfall, Agile-ish methodologies need a plan as well.

**What is Waterfall Methodology good for?**

Building a Nuclear Power Plant.

**What is Agile in a nutshell?**

Either of two (and very rarely both):

1. Currently, quite a fashionable social ritual.
2. A reasonably successful attempt to apply ideas and principles widely used in areas of human activity with a naturally high level of uncertainty to the process of software development.

For more details I would recommend a talk from [Pragmatic Dave Thomas](https://www.youtube.com/watch?v=a-BOSpxYJ9M&amp;t=149s), who was one of the signers of the original Agile Manifesto and now calls Scrum "an industry for producing Scrum Masters" (c). 
Long story short, understanding the principles and ideas led to them is far more important than doing "morning stand-ups" or "planning poker".

**No, seriously, Agile or not Agile?**

Let's make a small step back and look into the principles for dealing with natural and constant uncertainties in entrepreneurship, military, genetic algorithms, etc:

- It is almost impossible to precisely predict the future.
- With a limited number of resources and uncertainty from a changing landscape around it, it is impossible to fix both "scope of work" and "cost" - one will inevitably suffer.
- Focusing on fewer tasks minimizes context-switching waste.
- Small groups require way less communication compared to big ones.
- An adaptive course of actions is fundamentally simple:
   1. Understand where are you trying to get to
   2. Identify where you stand currently
   3. Of all available actions, pick and execute one with best impact/cost ratio ("Pareto 80/20" principle usually work quite well here as a fitting function)
   4. Validate the result of the action
   5. Iterate from step 1 if not done

This is what, in a nutshell, was the idea behind the Agile Manifesto.

**OK, then Scrum or Kanban?**

If you already have an established process in place, then start from Kanban (it was created to find bottlenecks).

If starting greenfield then go for Scrum (it will artificially tell you when your iteration should finish if you don't have a naturally fit boundary).

Scrumban - if neither worked but you still want to follow the "formally Agile" ritual.

But if not, just create a simple plan, understand and follow the principles above, take and shape some of the Agile techniques to positively fit into your organisation, using common sense.

Also be close to your customer and just automate it with DevOps, targeting Continuous Delivery.

**Functional Programming or Object Oriented?**

A good developer, these days, should be able to use both in areas of their strengths. Most of the modern languages in their latest state allow both in some form. Try to benefit from "zero-cost abstractions" where they are available (Kotlin, Rust, C#). And try not to sacrifice performance for no good reason.

**When an IT project most likely will either fail or cost too much?**

When the responsibility (to deliver) is split from the authority (of making decisions).

**Do you really think anyone would read it till here?**

Not really. But you did, and in the our f2f we can skip the boring part and start discussing how I can help _you_.

[Some old test results](2021_05_21-Old_test_results.md)
