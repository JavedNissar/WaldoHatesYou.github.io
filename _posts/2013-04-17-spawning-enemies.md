---
layout: post
---
A while ago, I was working on my game, trying to get the game to spawn
more enemies as time passed. It didn't take long for me to realize that
the best way to accomplish this was to use an exponential function that would
take the number of times that the enemy has spawned since the game
started as an input and then output a number that would act as the
interval at which enemies would spawn. I realized that this was easy to
code and easy to reason about, which made it perfect for my game,
so I quickly wrote up the code and added it to a spawner game object
in Unity3D and then I was done. The code itself is written in C# and
takes a few different parameters.
{%highlight C# %}
//exponential function that dictates the interval at which asteroids spawn
	float calculateNewInterval(float yintercept,float asymptote,float b,int numberOfSpawns){
		return (yintercept-asymptote)*Mathf.Pow(b,(-1F/stretch)*numberOfSpawns)+asymptote;
	}
{% endhighlight %}
![Graph of Exponential Function](/images/GraphOfEnemySpawningFunction.jpg)
In the code, *yintercept* is the point at which the exponential function
crosses the y-axis if it was graphed on the cartesian plane
(also known as the y-intercept). Meanwhile, the *asymptote* is the value
that the exponential value never reaches and *stretch* does exactly what
it implies, it stretches the function so that it takes longer to reach
a particular value than it would otherwise. Finally, *b* is the base of
the exponential function (I usually set 2 to be the base) and *numberOfSpawns*
 is the input that I mentioned earlier.

Regardless, the reason that the exponential function is flipped on the
y-axis (as shown by the the expression *(-1F/stretch)*) is to ensure
that the interval decreases over time. In addition, the reason
*(yintercept-asymptote)* is the coefficient applied to the function is
because the y-intercept of an exponential function is equal to the sum of
the coefficient of the base and the asymptote.
