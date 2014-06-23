---
layout: post
---
A while ago, I was working on my game, trying to get it to spawn more enemies as time passed. It didn't take long for me to realize that the best way to accomplish this feat was to use an exponential function that would take the number of times that the enemy has spawned since the game started as an input and then output a number that would act as the interval at which enemies would spawn. I realized that this was easy to code and I thought it was pretty clever so I quickly wrote up the code and added it to a game object in Unity3D. The code itself is
written in C# and it takes a few different parameters.
{%highlight C# %}
//exponential function that dictates the interval at which asteroids spawn
float calculateNewInterval(float yintercept,float asymptote,float b,int numberOfSpawns){
	return (yintercept-asymptote)*Mathf.Pow(b,(-1F/stretch)*numberOfSpawns)+asymptote;
}
{% endhighlight %}
In the code, the *yintercept* variable is the point at which the exponential function crosses the y-axis if it was graphed on the cartesian plane. Meanwhile,
the *asymptote* variable is the value that the exponential function will never output (although it will get closer to it over time), this is a fundamental property of exponential functions and if you want, you can learn more about the properties of exponential functions [here](http://en.wikipedia.org/wiki/Exponential_function). Regardless, the *stretch* variable does exactly what it implies, it horizontally stretches the function so that it takes longer to reach a particular value than it would otherwise. Finally, the *b* variable is the base of the exponential function (I usually set 2 to be the base) and *numberOfSpawns* is the number of enemies that have been spawned at that point in the game.  

![Graph of Exponential Function](/images/GraphOfEnemySpawningFunction.jpg)  

Nevertheless, as you can see in the graph above, the exponential function described in the code above is decreasing as the input increases (the input is represented by the x-axis). This occurs because the exponential function is flipped on the y-axis unlike a standard exponential function which is increasing as the input increases. That being said, the flip on the y-axis occurs because of the expression *(-1F/stretch)*. In addition, the reason *(yintercept-asymptote)* is the coefficient applied to the function is because the y-intercept (the point at which a one dimensional function crosses the y-axis) of an exponential function is equal to the sum of the coefficient of the base and the asymptote. Therefore, to ensure that the y-intercept is a particular value, the value of the asymptote must be subtracted from the y-intercept to determine the coefficient.
