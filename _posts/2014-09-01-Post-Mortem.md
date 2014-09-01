---
layout: post
---
At the beginning of August, I launched a mobile arcade game named [GRB](http://www.grbgame.com). At that point, I had been working on GRB for the past six months and I was exhausted. Before launch, I made sure that every day I got home from school at least an hour of my time would be devoted to GRB and on the weekends (as well as during summer break) I would work on the game until I no longer had the will to work on it anymore. This arrangement served me well and I enjoyed every moment that I spent working on GRB; however, at this point in time, GRB is clearly a failure. Currently, I have only 377 downloads across Google Play and the Apple App Store. After a single week, I lost more than three quarters of my initial user base and the new customers I gained didn't even come close to making up for my initial losses; thereby, showing that even if I got new customers there are fundamental problems with the game's design that prevent it from retaining users. Ever since I came to this realization, I've been trying to determine exactly what went wrong when I created GRB. What you see below is the conclusions of my analysis of GRB's development and release.
What Went Wrong
---
-	Failure to solicit feedback early

	I now realize that I should have sought feedback early in the development of GRB and that I should have posted a prototype to communities such as reddit's /r/gamedev as well as sending preview copies to gaming sites like SlideToPlay. In addition, I should have been open about the development of the game on social networks like Twitter, and Google+.

-	Not thinking carefully about how the game would gain users

	After I realized that GRB is a failure, I started reading The Lean Startup (a book about a particular method of building companies by Eric Ries) and my favorite part was the section where the author wrote about growth engines and how different products grab the majority of their users in different ways. For example, a site that sells shoes might focus on acquiring users through paid advertisements while a video game developer might focus on acquiring users through social media. When I was developing GRB, I assumed that if anyone liked it they would just talk about it without any action on my part but I now understand that if I want to acquire users through social networking sites I should have given users the ability to share their score and I should have promoted the game more on those sites.
	
-	Focusing on unimportant details

	There was a point in the development of GRB where I realized that the procedural background generation algorithm I used would occassionally spawn stars so that they were intersecting with another star. It really wasn't that noticeable but to me the flaw in my algorithm created an unholy abomination and I spent an entire week trying to find a solution for a problem that I never solved and never received complaints for.


What Went Right
---

-	Version Control

	I used git religiously throughout the development of GRB, every time I finished a feature I would commit the project in order to ensure that I had the option to revert to an earlier snapshot of the project at any time. This habit of mine allowed me to easily backtrack whenever I made a mistake.
	
-	Choosing to use Unity

	At the time I started development of GRB, Unity Technologies had only just added 2D game development to Unity's list of features. At first, I thought choosing Unity would be a bad idea because of how new the 2D game development feature was, but thanks to my experience developing GRB I've found that Unity is incredible for 2D game development due to the variety of plugins available for Unity and the ability to use C# (one of my favorite programming languages) for development.
	