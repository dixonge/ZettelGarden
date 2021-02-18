# A Recipe Spreadsheet - Sourdough

Created: Mar 24, 2017 7:46 AM
URL: https://sourdough.com/forum/recipe-spreadsheet
Updated: Mar 24, 2017 7:54 AM

# A Recipe Spreadsheet

[PhilBakerAdams](https://sourdough.com/philbakeradams) 2014 June 16

![[A%20Recipe%20Spreadsheet%20-%20Sourdough%200239b1b6a70347ceb2a1815aff5ec012 aa5df3d6ac7b72cfe664ef157c5852db.jpg]]

I have been using a recipe spreasheet I've built for some while now - I thought other might find it useful.

You can use it to:

- Catalogue your recipes
- Easily scale a given recipe's quantities to a different target weight
- See the Baker's % of your recipes
- See the Hydration % of your recipes
- Use a starter of know hydration, which will correctly adjust the Baker's % & Hydration of the recipe
- Keep track of your baking when you print a recipe for use in the kitchen
- Keep notes
- Star-rate your recipe for Crust, Crumb and Taste qualities

If you find it useful, feel free to pass it on - all I ask is that you mention from where it came - thanks![http://www.bread.progtech.co.uk/index.htm](http://www.bread.progtech.co.uk/index.htm) 

[Recipe Ideas](https://sourdough.com/forum/recipe-ideas)

## Replies

![[A%20Recipe%20Spreadsheet%20-%20Sourdough%200239b1b6a70347ceb2a1815aff5ec012 6b2c1801e67a700e9cc936dea9d8c76f.jpg]]

[farinam](https://sourdough.com/farinam)

[2014 June 16](https://sourdough.com/forum/recipe-spreadsheet#comment-16731)

Hello PhilBakerAdams,

Nice looking spreadsheet. Haven't yet delved into the nitty gritty in any great detail but I can see one small problem with the water requirements for the target hydrations specifically when you enter the base loaf weight as the target (I haven't checked other cases). According to my calculations if you added the amount shown for say a typical 1kg loaf you would end up with a lower hydration (admittedly not a great deal different) than that indicated. In the case that I used, I calculate that the indicated amount for 74% (actual 74.49) should really be 73% (actual 73.39). I think it comes about because you pro rata the water based on the hydration ratios rather than calculating the water requirement from the flour amount with allowance for any in the starter.

In the scheme of things it doesn't matter a great deal but me being something of a pedant in these matters, I thought I would mention it.

As an aside, I have a hydration calculator linked to in one of my blogs here and I did make a start on a more comprehensive one such as you have done but got side tracked onto other things and never completed it.

So, well done and good luck with your projects.

Farinam

.

[PhilBakerAdams](https://sourdough.com/philbakeradams) [2014 June 17](https://sourdough.com/forum/recipe-spreadsheet#comment-16733) 

Hi - thanks for the comment.I'm not sure what the arithmetic was there, but I do know I was using a clumsy kludge for adding the Sourdough Hydration - so you comment spurred me on to make the necessary corrections - the revised version now (I hope!) does work things out correctly.

.

![[A%20Recipe%20Spreadsheet%20-%20Sourdough%200239b1b6a70347ceb2a1815aff5ec012 6b2c1801e67a700e9cc936dea9d8c76f.jpg]]

[farinam](https://sourdough.com/farinam)

[2014 June 17](https://sourdough.com/forum/recipe-spreadsheet#comment-16734)

Hi PhilBakerAdams,

I can't see that your new version is any different with respect to what i was talking about. To correct the small error, in cell J5 et seq you need a formula like

=IF(WaterWanted<>"",((WaterWanted+Starter*0.5)/RecipePercent) *L5 - Starter*0.5,"")

Obviously, the multiplier for the starter needs to be variable so you would need to convert the StarterWater cell from a string to a value and use that perhaps.

As I say it is not a great drama, it only makes a percent or two difference in the amount of water needed so if you don't feel the need, the world is not going to end.

Good luck with your projects.

Farinam

.

[PhilBakerAdams](https://sourdough.com/philbakeradams) [2014 June 19](https://sourdough.com/forum/recipe-spreadsheet#comment-16735) 

Ah! Thanks, Farinam, I see what you mean.You know, smaller errors have caused greater havoc now and again ;-)So the latest version, with the proper Starter hydration calculation, and now also with the Target hydration corrected as per Farinam's observation, is in place.My web-hosting package appears to be playing silly beggars with the page, so if anyone wants to give it a try and hasn't been able to access it, it's also available via my Google Drive: [https://drive.google.com/file/d/0B27iARW0qIktSWhuLWJmN3c0MXc/edit?usp=sharing](https://drive.google.com/file/d/0B27iARW0qIktSWhuLWJmN3c0MXc/edit?usp=sharing)

.

![[A%20Recipe%20Spreadsheet%20-%20Sourdough%200239b1b6a70347ceb2a1815aff5ec012 6b2c1801e67a700e9cc936dea9d8c76f.jpg]]

[farinam](https://sourdough.com/farinam)

[2014 June 19](https://sourdough.com/forum/recipe-spreadsheet#comment-16736)

Hi Phil,

Your summation in F18 includes the starter flour calculation in F9 and gives an incorrect dough mass.

Also, strictly, the correction should also be applied to the Other Liquid calculation as well. Plus, you should be working on the scaled starter mass rather than the original starter mass.

Keep on bakin' ( and spreadsheetin')

Farinam

.

![[A%20Recipe%20Spreadsheet%20-%20Sourdough%200239b1b6a70347ceb2a1815aff5ec012 6b2c1801e67a700e9cc936dea9d8c76f.jpg]]

[farinam](https://sourdough.com/farinam)

[2014 June 20](https://sourdough.com/forum/recipe-spreadsheet#comment-16737)

Hi Phil,

Thinking through it all, can I make the following suggestions.

Name cell G10 WaterRatio , G11 OtherRatio and I9 ScaledStarterRatio.

I9 formula is copied down from I8.

J5 et seq becomes =((SUM(TargetFlours)-ScaledStarterWater)*L5-ScaledStarterWater)*WaterRatio

K5 et seq becomes =((SUM(TargetFlours)-ScaledStarterWater)*L5-ScaledStarterWater)*OtherRatio

I think it is more understandable to calculate the liquid from the actual flour and target hydration rather than going the other path. Of course, if you maintain the dry ingredient mass and change the liquid the mass of the final dough will be different from the 'target'. So, arguably, the liquid requirements for hydration variation should be calculated from the original recipe and adjusted using the appropriate 'scale factor' for the different mass involved.

Your group percentages for flour in G5 et seq could become =IF(F5>0,F5/(FlourOne+FlourTwo+FlourThree+(Starter/StarterFlourAndWater)),"")

And for the starter in G8 could become =IF(F8>0,F8/(FlourOne+FlourTwo+FlourThree+(Starter/StarterFlourAndWater))/StarterFlourAndWater,""). This assumes of course that you want the group percentages to add to 100%.

Complicated, hey!

Farinam

.

## Post Reply

Already a member? [Login](https://sourdough.com/user?destination=node/27835)

![[A%20Recipe%20Spreadsheet%20-%20Sourdough%200239b1b6a70347ceb2a1815aff5ec012 9db1be49d5e50c53704eb298615a7c3a.jpg]]

The content of this field is kept private and will not be shown publicly.

Source

Format

 **Upload Photo**

.

Files must be less than **64 MB**.Allowed file types: **png gif jpg jpeg**.