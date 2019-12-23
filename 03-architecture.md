# Fire up the IDE...You have your marching orders, now GO CODE!  

## not so fast...

Before you open your IDE, you should have 1 billion questions, to ask. And this request came from the business.  It is the equivalent of "build me a house, and I don't care how you do it". But they do care greatly *HOW* it functions, but not the materials per se.  2, 3 or 5 bedrooms? 1 story or 2 story. Time to start asking questions. They business team know everything about pricing, inventory, and retail accounting, but zippo about technology.  To make a decision, you first need to understand your options and what they want (and what they are willing to pay for).  What if you went to Chipotle and they took down their menu, but you still had to order?  You would end up asking lots of question. 

We have an old joke in IT when projects start:  Good, Fast, Cheap: Pick two and the other goes the wrong direction. :D 

#### Start with a Whiteboard (or pen and paper)

The most basic pattern of business software that has evolved over the last few decades is the 3 tier architecture.  It allows `Seperation of Concerns` between:  
* Frontend: Showing the data (browser)
* Backend: Processing the data (server)
* Storage: Storing the data (database)

In theory (but rarely in practice), each tier can be swapped out without impact to the other tiers.

[Front and Backends (wikipedia)](https://en.wikipedia.org/wiki/Front_and_back_ends)

## Three Tier Architecture

For simplicity, we will stay hard inside this 3 tier architecture, and as we needed, we will just add layers inside each of the tiers. 

![](03-3-layer-architecture.png)

So just like the Chipotle choices, in the begining, you can independently choose what you want for each option.  Taco + Steak + Guac or Burrito + Chicken + Corn Salsa. Once it is made, it is hard to swap out, so I can't stress enough, that if you aren't sure, consult somebody who has been punched in the nose a few times. It will save you tons of heart ache, late nights and slobbering crying.   I promise.   Erasing a line on the whiteboard at the begining of the project is alot easier (and cheaper) than refactoring a major component 3 months in because you didn't take volumne into consideration. 

So I like to work "bottom up" on these.  Why? Because `Data has gravity` [[link]](https://www.cio.com/article/3331604/data-gravity-and-what-it-means-for-enterprise-data-analytics-and-ai-architectures.html).  You can have the prettiest UI in the world, but if you data is slow to acccess or unreliable, then it doesn't matter. 

## Microservices and REST

A quick note from an "old guy", technology history is fun to me. You really can't understand where somebody is unless you understand where they came from and what path they traveled.  Technology has created a very full graveyard of libraries, companies, hardware, platforms, etc. So the following two words get toss around, and although they are great, what they really are is much better than their predecesors. 

**Microservices**  microservices was a pendelum swing from the "monolith". Projects 10+ years ago, were built as 1 BIG application.  `The inventory app`.  It was 10,000s of lines of code, and all deployed at once. Deploying it was a 12 hour affair, that happened overnight, with 20 people in a room and another 30 on call with all these super complicated "backout plans".  It was a nasty slow business. 

Enter microservices. The idea was to "break apart' the monolith into small tiny "microservices" and each microservice could be independtently deployed, scaled, and rolled back. One of the best things this did for us was halt the dreaded `overnight deployment`

Enter REST, if you are going to break apart the monolith to microservices, then you need to define a clean way for these microservices to inter-communicate. REST is a wonderful, clean standard, using HTTP protocol to define the way things "talk" to each other.  Generally it is between Frontend and Backend, and from Backend to other Backends.  The database us usually a proprietary protocol or JDBC. 


## [NEXT -->](04-database.md)