# Swirl-Exploratory-Data-Analysis-Lesson-5
| Base_Plotting_System. (Slides for this and other Data Science courses may be found
| at github https://github.com/DataScienceSpecialization/courses/. If you care to use
| them, they must be downloaded as a zip file and viewed locally. This lesson
| corresponds to 04_ExploratoryAnalysis/PlottingBase.)

...


  |                                                                                   
  |=                                                                            |   2%
| In another lesson, we gave you an overview of the three plotting systems in R. In
| this lesson we'll focus on the base plotting system and talk more about how you can
| exploit all its many parameters to get the plot you want.  We'll focus on using the
| base plotting system to create graphics on the screen device rather than another
| graphics device.

...


  |                                                                                   
  |==                                                                           |   3%
| The core plotting and graphics engine in R is encapsulated in two packages. The
| first is the graphics package which contains plotting functions for the "base"
| system. The functions in this package include plot, hist, boxplot, barplot, etc. The
| second package is grDevices which contains all the code implementing the various
| graphics devices, including X11, PDF, PostScript, PNG, etc.

...


  |                                                                                   
  |====                                                                         |   5%
| Base graphics are often constructed piecemeal, with each aspect of the plot handled
| separately through a particular function call. Usually you start with a plot
| function (such as plot, hist, or boxplot), then you use annotation functions (text,
| abline, points) to add to or modify your plot.

...


  |                                                                                   
  |=====                                                                        |   6%
| Before making a plot you have to determine where the plot will appear and what it
| will be used for.  Is there a large amount of data going into the plot? Or is it
| just a few points? Do you need to be able to dynamically resize the graphic?

...


  |                                                                                   
  |======                                                                       |   8%
| What do you think is a disadvantage of the Base Plotting System?

1: It mirrors how we think of building plots and analyzing data
2: It's intuitive and exploratory
3: You can't go back once a plot has started
4: A complicated plot is a series of simple R commands

Selection: 3

| You're the best!


  |                                                                                   
  |=======                                                                      |   9%
| Yes! The base system is very intuitive and easy to use. You can't go backwards,
| though, say, if you need to readjust margins or have misspelled a caption. A
| finished plot will be a series of R commands, so it's difficult to translate a
| finished plot into a different system.

...


  |                                                                                   
  |========                                                                     |  11%
| Calling a basic routine such as plot(x, y) or hist(x) launches a graphics device (if
| one is not already open) and draws a new plot on the device. If the arguments to
| plot or hist are not of some special class, then the default method is called.

...


  |                                                                                   
  |=========                                                                    |  12%
| As you'll see, most of the base plotting functions have many arguments, for example,
| setting the title, labels of axes, plot character, etc. Some of the parameters can
| be set when you call the function or they can be added later in a separate function
| call.

...


  |                                                                                   
  |==========                                                                   |  14%
| Now we'll go through some quick examples of basic plotting before we delve into gory
| details. We'll use the dataset airquality (part of the library datasets) which we've
| loaded for you. This shows ozone and other air measurements for New York City for 5
| months in 1973.

...


  |                                                                                   
  |============                                                                 |  15%
| Use the R command head with airquality as an argument to see what the data looks
| like.

> head(airquality)
  Ozone Solar.R Wind Temp Month Day
1    41     190  7.4   67     5   1
2    36     118  8.0   72     5   2
3    12     149 12.6   74     5   3
4    18     313 11.5   62     5   4
5    NA      NA 14.3   56     5   5
6    28      NA 14.9   66     5   6

| All that practice is paying off!


  |                                                                                   
  |=============                                                                |  17%
| We see the dataset contains 6 columns of data. Run the command range with two
| arguments. The first is the ozone column of airquality, specified by
| airquality$Ozone, and the second is the boolean na.rm set equal to TRUE. If you
| don't specify this second argument, you won't get a meaningful result.

> range(airqulity$Ozone, na.rm = TRUE)
Error: object 'airqulity' not found
> range(airquality$Ozone, na.rm = TRUE)
[1]   1 168

| Nice work!


  |                                                                                   
  |==============                                                               |  18%
| So the measurements range from 1 to 168. First we'll do a simple histogram of this
| ozone column to show the distribution of measurements. Use the R command hist with
| the argument airquality$Ozone.

> hist(airquality$Ozone)

| Perseverance, that's the answer.


  |                                                                                   
  |===============                                                              |  20%
| Simple, right? R put a title on the histogram and labeled both axes for you. What is
| the most frequent count?

1: Over 100
2: Under 25
3: Between 60 and 75
4: Over 150

Selection: 2

| All that practice is paying off!


  |                                                                                   
  |================                                                             |  21%
| Next we'll do a boxplot. First, though, run the R command table with the argument
| airquality$Month.

> table(airquality$Month)

 5  6  7  8  9 
31 30 31 31 30 

| That's correct!


  |                                                                                   
  |==================                                                           |  23%
| We see that the data covers 5 months, May through September. We'll want a boxplot of
| ozone as a function of the month in which the measurements were taken so we'll use
| the R formula Ozone~Month as the first argument of boxplot. Our second argument will
| be airquality, the dataset from which the variables of the first argument are taken.
| Try this now.

> boxplot(Ozone~Month, airquality)

| You are amazing!


  |                                                                                   
  |===================                                                          |  24%
| Note that boxplot, unlike hist, did NOT specify a title and axis labels for you
| automatically.

...


  |                                                                                   
  |====================                                                         |  26%
| Let's call boxplot again to specify labels. (Use the up arrow to recover the
| previous command and save yourself some typing.) We'll add more arguments to the
| call to specify labels for the 2 axes. Set xlab equal to "Month" and ylab equal to
| "Ozone (ppb)". Specify col.axis equal to "blue" and col.lab equal to "red". Try this
| now.

> boxplot(xlab = "Month", ylab = "Ozone(ppb)", col.axis = "blue", col.lab ="red")
Error in boxplot.default(xlab = "Month", ylab = "Ozone(ppb)", col.axis = "blue",  : 
  argument "x" is missing, with no default
> boxplot(Ozone~Month, airquality, plot(xlab = "Month", ylab = "Ozone(ppb)", col.axis = "blue", col.lab ="red"))
Error in xy.coords(x, y, xlabel, ylabel, log) : 
  argument "x" is missing, with no default
> boxplot(Ozone~Month, airquality, "Month", "Ozone(ppb)", col.axis = "blue", col.lab ="red"))
Error: unexpected ')' in "boxplot(Ozone~Month, airquality, "Month", "Ozone(ppb)", col.axis = "blue", col.lab ="red"))"
> boxplot
function (x, ...) 
UseMethod("boxplot")
<bytecode: 0x00000000181c3de0>
<environment: namespace:graphics>

| That's not exactly what I'm looking for. Try again. Or, type info() for more
| options.

| Type boxplot(Ozone~Month, airquality, xlab="Month", ylab="Ozone
| (ppb)",col.axis="blue",col.lab="red") at the command prompt.

> boxplot(Ozone~Month, airquality, xlab="Month", ylab="Ozone(ppb)", col.axis = "blue", col.lab ="red"))
Error: unexpected ')' in "boxplot(Ozone~Month, airquality, xlab="Month", ylab="Ozone(ppb)", col.axis = "blue", col.lab ="red"))"
> boxplot(Ozone~Month, airquality, xlab="Month", ylab="Ozone(ppb)", col.axis = "blue", col.lab ="red")

| That's not the answer I was looking for, but try again. Or, type info() for more
| options.

| Type boxplot(Ozone~Month, airquality, xlab="Month", ylab="Ozone
| (ppb)",col.axis="blue",col.lab="red") at the command prompt.

> boxplot(Ozone~Month, airquality, xlab="Month", ylab="Ozone(ppb)",col.axis="blue",col.lab="red")

| Not quite right, but keep trying. Or, type info() for more options.

| Type boxplot(Ozone~Month, airquality, xlab="Month", ylab="Ozone
| (ppb)",col.axis="blue",col.lab="red") at the command prompt.

> boxplot(Ozone~Month, airquality, xlab="Month", ylab="Ozone(ppb)",col.axis="blue",col.lab="red")

| Give it another try. Or, type info() for more options.

| Type boxplot(Ozone~Month, airquality, xlab="Month", ylab="Ozone
| (ppb)",col.axis="blue",col.lab="red") at the command prompt.

> reset()
Error in UseMethod("do_rst") : 
  no applicable method for 'do_rst' applied to an object of class "c('environment', 'default')"

| Leaving swirl now. Type swirl() to resume.

> swirl()

| Welcome to swirl! Please sign in. If you've been here before, use the same name as
| you did then. If you are new, call yourself something unique.

What shall I call you? g

| Would you like to continue with one of these lessons?

1: Exploratory Data Analysis Base Plotting System
2: No. Let me start something new.

Selection: 1


| Let's call boxplot again to specify labels. (Use the up arrow to recover the
| previous command and save yourself some typing.) We'll add more arguments to the
| call to specify labels for the 2 axes. Set xlab equal to "Month" and ylab equal to
| "Ozone (ppb)". Specify col.axis equal to "blue" and col.lab equal to "red". Try this
| now.

> boxplot(Ozone~Month, airquality, xlab="Month", ylab="Ozone(ppb)",col.axis="blue",col.lab="red")

| Not quite right, but keep trying. Or, type info() for more options.

| Type boxplot(Ozone~Month, airquality, xlab="Month", ylab="Ozone
| (ppb)",col.axis="blue",col.lab="red") at the command prompt.

> boxplot(Ozone~Month, airquality, xlab = "Month", ylab = "Ozone (ppb)", col.axis = "blue", col.lab = "red")

| Great job!


  |                                                                                   
  |=====================                                                        |  27%
| Nice colors, but still no title. Let's add one with the R command title. Use the
| argument main set equal to the string "Ozone and Wind in New York City".

> title(main = "Ozone and Wind in New York City")

| You are amazing!


  |                                                                                   
  |======================                                                       |  29%
| Now we'll show you how to plot a simple two-dimensional scatterplot using the R
| function plot. We'll show the relationship between Wind (x-axis) and Ozone (y-axis).
| We'll use the function plot with those two arguments (Wind and Ozone, in that
| order). To save some typing, though, we'll call the R command with using 2
| arguments. The first argument of with will be airquality, the dataset containing
| Wind and Ozone; the second argument will be the call to plot. Doing this allows us
| to avoid using the longer notation, e.g., airquality$Wind. Try this now.

> scatterplot(airqulity, dateset(Wind, Ozone))
Error in scatterplot(airqulity, dateset(Wind, Ozone)) : 
  could not find function "scatterplot"
> with(airquality, plot(Wind, Ozone))

| You are really on a roll!


  |                                                                                   
  |=======================                                                      |  30%
| Note that plot generated labels for the x and y axes but no title.

...


  |                                                                                   
  |========================                                                     |  32%
| Add one now with the R command title. Use the argument main set equal to the string
| "Ozone and Wind in New York City". (You can use the up arrow to recover the command
| if you don't want to type it.)

> title(main = "Ozone and Wind in New York City")

| You are really on a roll!


  |                                                                                   
  |==========================                                                   |  33%
| The basic plotting parameters are documented in the R help page for the function
| par. You can use par to set parameters OR to find out what values are already set.
| To see just how much flexibility you have, run the R command length with the
| argument par() now.

> par()
$xlog
[1] FALSE

$ylog
[1] FALSE

$adj
[1] 0.5

$ann
[1] TRUE

$ask
[1] FALSE

$bg
[1] "transparent"

$bty
[1] "o"

$cex
[1] 1

$cex.axis
[1] 1

$cex.lab
[1] 1

$cex.main
[1] 1.2

$cex.sub
[1] 1

$cin
[1] 0.15 0.20

$col
[1] "black"

$col.axis
[1] "black"

$col.lab
[1] "black"

$col.main
[1] "black"

$col.sub
[1] "black"

$cra
[1] 14.4 19.2

$crt
[1] 0

$csi
[1] 0.2

$cxy
[1]  0.7519544 10.3568369

$din
[1] 5.333333 5.322917

$err
[1] 0

$family
[1] ""

$fg
[1] "black"

$fig
[1] 0 1 0 1

$fin
[1] 5.333333 5.322917

$font
[1] 1

$font.axis
[1] 1

$font.lab
[1] 1

$font.main
[1] 2

$font.sub
[1] 1

$lab
[1] 5 5 7

$las
[1] 0

$lend
[1] "round"

$lheight
[1] 1

$ljoin
[1] "round"

$lmitre
[1] 10

$lty
[1] "solid"

$lwd
[1] 1

$mai
[1] 1.02 0.82 0.82 0.42

$mar
[1] 5.1 4.1 4.1 2.1

$mex
[1] 1

$mfcol
[1] 1 1

$mfg
[1] 1 1 1 1

$mfrow
[1] 1 1

$mgp
[1] 3 1 0

$mkh
[1] 0.001

$new
[1] FALSE

$oma
[1] 0 0 0 0

$omd
[1] 0 1 0 1

$omi
[1] 0 0 0 0

$page
[1] TRUE

$pch
[1] 1

$pin
[1] 4.093333 3.482917

$plt
[1] 0.1537500 0.9212500 0.1916243 0.8459491

$ps
[1] 12

$pty
[1] "m"

$smo
[1] 1

$srt
[1] 0

$tck
[1] NA

$tcl
[1] -0.5

$usr
[1]   0.94  21.46  -5.68 174.68

$xaxp
[1]  5 20  3

$xaxs
[1] "r"

$xaxt
[1] "s"

$xpd
[1] FALSE

$yaxp
[1]   0 150   3

$yaxs
[1] "r"

$yaxt
[1] "s"

$ylbias
[1] 0.2


| Almost! Try again. Or, type info() for more options.

| Type length(par()) at the command prompt.

> length(par())
[1] 72

| You nailed it! Good job!


  |                                                                                   
  |===========================                                                  |  35%
| So there are a boatload (72) of parameters that par() gives you access to. Run the R
| function names with par() as its argument to see what these parameters are.

> par()
$xlog
[1] FALSE

$ylog
[1] FALSE

$adj
[1] 0.5

$ann
[1] TRUE

$ask
[1] FALSE

$bg
[1] "transparent"

$bty
[1] "o"

$cex
[1] 1

$cex.axis
[1] 1

$cex.lab
[1] 1

$cex.main
[1] 1.2

$cex.sub
[1] 1

$cin
[1] 0.15 0.20

$col
[1] "black"

$col.axis
[1] "black"

$col.lab
[1] "black"

$col.main
[1] "black"

$col.sub
[1] "black"

$cra
[1] 14.4 19.2

$crt
[1] 0

$csi
[1] 0.2

$cxy
[1]  0.7519544 10.3568369

$din
[1] 5.333333 5.322917

$err
[1] 0

$family
[1] ""

$fg
[1] "black"

$fig
[1] 0 1 0 1

$fin
[1] 5.333333 5.322917

$font
[1] 1

$font.axis
[1] 1

$font.lab
[1] 1

$font.main
[1] 2

$font.sub
[1] 1

$lab
[1] 5 5 7

$las
[1] 0

$lend
[1] "round"

$lheight
[1] 1

$ljoin
[1] "round"

$lmitre
[1] 10

$lty
[1] "solid"

$lwd
[1] 1

$mai
[1] 1.02 0.82 0.82 0.42

$mar
[1] 5.1 4.1 4.1 2.1

$mex
[1] 1

$mfcol
[1] 1 1

$mfg
[1] 1 1 1 1

$mfrow
[1] 1 1

$mgp
[1] 3 1 0

$mkh
[1] 0.001

$new
[1] FALSE

$oma
[1] 0 0 0 0

$omd
[1] 0 1 0 1

$omi
[1] 0 0 0 0

$page
[1] TRUE

$pch
[1] 1

$pin
[1] 4.093333 3.482917

$plt
[1] 0.1537500 0.9212500 0.1916243 0.8459491

$ps
[1] 12

$pty
[1] "m"

$smo
[1] 1

$srt
[1] 0

$tck
[1] NA

$tcl
[1] -0.5

$usr
[1]   0.94  21.46  -5.68 174.68

$xaxp
[1]  5 20  3

$xaxs
[1] "r"

$xaxt
[1] "s"

$xpd
[1] FALSE

$yaxp
[1]   0 150   3

$yaxs
[1] "r"

$yaxt
[1] "s"

$ylbias
[1] 0.2


| Not quite! Try again. Or, type info() for more options.

| Type names(par()) at the command prompt.

> names(par())
 [1] "xlog"      "ylog"      "adj"       "ann"       "ask"       "bg"       
 [7] "bty"       "cex"       "cex.axis"  "cex.lab"   "cex.main"  "cex.sub"  
[13] "cin"       "col"       "col.axis"  "col.lab"   "col.main"  "col.sub"  
[19] "cra"       "crt"       "csi"       "cxy"       "din"       "err"      
[25] "family"    "fg"        "fig"       "fin"       "font"      "font.axis"
[31] "font.lab"  "font.main" "font.sub"  "lab"       "las"       "lend"     
[37] "lheight"   "ljoin"     "lmitre"    "lty"       "lwd"       "mai"      
[43] "mar"       "mex"       "mfcol"     "mfg"       "mfrow"     "mgp"      
[49] "mkh"       "new"       "oma"       "omd"       "omi"       "page"     
[55] "pch"       "pin"       "plt"       "ps"        "pty"       "smo"      
[61] "srt"       "tck"       "tcl"       "usr"       "xaxp"      "xaxs"     
[67] "xaxt"      "xpd"       "yaxp"      "yaxs"      "yaxt"      "ylbias"   

| Great job!


  |                                                                                   
  |============================                                                 |  36%
| Variety is the spice of life. You might recognize some of these such as col and lwd
| from previous swirl lessons. You can always run ?par to see what they do. For now,
| run the command par()$pin and see what you get.

> ?par
> par()$pin
[1] 4.093333 3.482917

| All that practice is paying off!


  |                                                                                   
  |=============================                                                |  38%
| Alternatively, you could have gotten the same result by running par("pin") or
| par('pin')).  What do you think these two numbers represent?

1: Plot dimensions in inches
2: Coordinates of the center of the plot window
3: Random numbers
4: A confidence interval

Selection: 4

| Almost! Try again.

| The function par specifies graphical parameters so the answer should deal with
| plots. That leaves two choices. The 'in' in 'pin' specifies inches.

1: Coordinates of the center of the plot window
2: Plot dimensions in inches
3: Random numbers
4: A confidence interval

Selection: 1

| Almost! Try again.

| The function par specifies graphical parameters so the answer should deal with
| plots. That leaves two choices. The 'in' in 'pin' specifies inches.

1: Plot dimensions in inches
2: Random numbers
3: A confidence interval
4: Coordinates of the center of the plot window

Selection: 2

| Not exactly. Give it another go.

| The function par specifies graphical parameters so the answer should deal with
| plots. That leaves two choices. The 'in' in 'pin' specifies inches.

1: Coordinates of the center of the plot window
2: Random numbers
3: A confidence interval
4: Plot dimensions in inches

Selection: 4

| You got it right!


  |                                                                                   
  |==============================                                               |  39%
| Now, run the command par("fg") or or par('fg') or par()$fg and see what you get.

> par("fg")
[1] "black"

| You are amazing!


  |                                                                                   
  |================================                                             |  41%
| It gave you a color, right? Since par()$fg specifies foreground color, what do you
| think par()$bg specifies?

1: Beautiful color
2: Better color
3: Background color
4: blue-green

Selection: 3

| Keep up the great work!


  |                                                                                   
  |=================================                                            |  42%
| Many base plotting functions share a set of parameters. We'll go through some of the
| more commonly used ones now. See if you can tell what they do from their names.

...


  |                                                                                   
  |==================================                                           |  44%
| What do you think the graphical parameter pch controls?

1: pc help
2: picture characteristics
3: plot character
4: point control height

Selection: 2

| Keep trying!

| The p stands for plot.

1: plot character
2: pc help
3: point control height
4: picture characteristics

Selection: 1

| You're the best!


  |                                                                                   
  |===================================                                          |  45%
| The plot character default is the open circle, but it "can either be a single
| character or an integer code for one of a set of graphics symbols." Run the command
| par("pch") to see the integer value of the default. When you need to, you can use
| R's Documentation (?pch) to find what the other values mean.

> par("pach")
NULL
Warning message:
In par("pach") : "pach" is not a graphical parameter

| Almost! Try again. Or, type info() for more options.

| Type par()$pch OR par('pch') OR par("pch") at the command prompt.

> par("pch")
[1] 1

| You are amazing!


  |                                                                                   
  |====================================                                         |  47%
| So 1 is the code for the open circle. What do you think the graphical parameters lty
| and lwd control respectively?

1: line width and type
2: line type and width
3: line length and width
4: line slope and intercept

Selection: 3

| Not quite right, but keep trying.

| The l obviously stands for line. The ty and wd should be obvious.

1: line type and width
2: line slope and intercept
3: line width and type
4: line length and width

Selection: 1

| Your dedication is inspiring!


  |                                                                                   
  |=====================================                                        |  48%
| Run the command par("lty") to see the default line type.

> par("lty")
[1] "solid"

| That's the answer I was looking for.


  |                                                                                   
  |======================================                                       |  50%
| So the default line type is solid, but it can be dashed, dotted, etc. Once again,
| R's ?par documentation will tell you what other line types are available. The line
| width is a positive integer; the default value is 1.

...


  |                                                                                   
  |========================================                                     |  52%
| We've seen a lot of examples of col, the plotting color, specified as a number,
| string, or hex code; the colors() function gives you a vector of colors by name.

...


  |                                                                                   
  |=========================================                                    |  53%
| What do you think the graphical parameters xlab and ylab control respectively?

1: labels for the x- and y- axes
2: labels for the y- and x- axes

Selection: 1

| Perseverance, that's the answer.


  |                                                                                   
  |==========================================                                   |  55%
| The par() function is used to specify global graphics parameters that affect all
| plots in an R session. (Use dev.off or plot.new to reset to the defaults.) These
| parameters can be overridden when specified as arguments to specific plotting
| functions. These include las (the orientation of the axis labels on the plot), bg
| (background color), mar (margin size), oma (outer margin size), mfrow and mfcol
| (number of plots per row, column).

...


  |                                                                                   
  |===========================================                                  |  56%
| The last two, mfrow and mfcol, both deal with multiple plots in that they specify
| the number of plots per row and column. The difference between them is the order in
| which they fill the plot matrix. The call mfrow will fill the rows first while mfcol
| fills the columns first.

...


  |                                                                                   
  |============================================                                 |  58%
| So to reiterate, first call a basic plotting routine. For instance, plot makes a
| scatterplot or other type of plot depending on the class of the object being
| plotted.

...


  |                                                                                   
  |==============================================                               |  59%
| As we've seen, R provides several annotating functions. Which of the following is
| NOT one of them?

1: points
2: hist
3: title
4: text
5: lines

Selection: 2

| All that hard work is paying off!


  |                                                                                   
  |===============================================                              |  61%
| So you can add text, title, points, and lines to an existing plot. To add lines, you
| give a vector of x values and a corresponding vector of y values (or a 2-column
| matrix); the function lines just connects the dots. The function text adds text
| labels to a plot using specified x, y coordinates.

...


  |                                                                                   
  |================================================                             |  62%
| The function title adds annotations. These include x- and y- axis labels, title,
| subtitle, and outer margin. Two other annotating functions are mtext which adds
| arbitrary text to either the outer or inner margins of the plot and axis which adds
| axis ticks and labels. Another useful function is legend which explains to the
| reader what the symbols your plot uses mean.

...


  |                                                                                   
  |=================================================                            |  64%
| Before we close, let's test your ability to make a somewhat complicated scatterplot.
| First run plot with 3 arguments. airquality$Wind, airquality$Ozone, and type set
| equal to "n". This tells R to set up the plot but not to put the data in it.

> scatterplot(airquality$Wind, airquality$Ozone, set = "n")
Error in scatterplot(airquality$Wind, airquality$Ozone, set = "n") : 
  could not find function "scatterplot"
> plot(airquality$Wind, airquality$Ozone, set = "n")
Warning messages:
1: In plot.window(...) : "set" is not a graphical parameter
2: In plot.xy(xy, type, ...) : "set" is not a graphical parameter
3: In axis(side = side, at = at, labels = labels, ...) :
  "set" is not a graphical parameter
4: In axis(side = side, at = at, labels = labels, ...) :
  "set" is not a graphical parameter
5: In box(...) : "set" is not a graphical parameter
6: In title(...) : "set" is not a graphical parameter

| Not exactly. Give it another go. Or, type info() for more options.

| Type plot(airquality$Wind, type="n",airquality$Ozone) at the command prompt.

> plot(airquality$Wind, type="n",airquality$Ozone)

| Excellent job!


  |                                                                                   
  |==================================================                           |  65%
| Now for the test. (You might need to check R's documentation for some of these.) Add
| a title with the argument main set equal to the string "Wind and Ozone in NYC"

> title(main = "Wind and Ozone in NYC")

| Great job!


  |                                                                                   
  |===================================================                          |  67%
| Now create a variable called may by subsetting airquality appropriately. (Recall
| that the data specifies months by number and May is the fifth month of the year.)

> subset(airquality)
    Ozone Solar.R Wind Temp Month Day
1      41     190  7.4   67     5   1
2      36     118  8.0   72     5   2
3      12     149 12.6   74     5   3
4      18     313 11.5   62     5   4
5      NA      NA 14.3   56     5   5
6      28      NA 14.9   66     5   6
7      23     299  8.6   65     5   7
8      19      99 13.8   59     5   8
9       8      19 20.1   61     5   9
10     NA     194  8.6   69     5  10
11      7      NA  6.9   74     5  11
12     16     256  9.7   69     5  12
13     11     290  9.2   66     5  13
14     14     274 10.9   68     5  14
15     18      65 13.2   58     5  15
16     14     334 11.5   64     5  16
17     34     307 12.0   66     5  17
18      6      78 18.4   57     5  18
19     30     322 11.5   68     5  19
20     11      44  9.7   62     5  20
21      1       8  9.7   59     5  21
22     11     320 16.6   73     5  22
23      4      25  9.7   61     5  23
24     32      92 12.0   61     5  24
25     NA      66 16.6   57     5  25
26     NA     266 14.9   58     5  26
27     NA      NA  8.0   57     5  27
28     23      13 12.0   67     5  28
29     45     252 14.9   81     5  29
30    115     223  5.7   79     5  30
31     37     279  7.4   76     5  31
32     NA     286  8.6   78     6   1
33     NA     287  9.7   74     6   2
34     NA     242 16.1   67     6   3
35     NA     186  9.2   84     6   4
36     NA     220  8.6   85     6   5
37     NA     264 14.3   79     6   6
38     29     127  9.7   82     6   7
39     NA     273  6.9   87     6   8
40     71     291 13.8   90     6   9
41     39     323 11.5   87     6  10
42     NA     259 10.9   93     6  11
43     NA     250  9.2   92     6  12
44     23     148  8.0   82     6  13
45     NA     332 13.8   80     6  14
46     NA     322 11.5   79     6  15
47     21     191 14.9   77     6  16
48     37     284 20.7   72     6  17
49     20      37  9.2   65     6  18
50     12     120 11.5   73     6  19
51     13     137 10.3   76     6  20
52     NA     150  6.3   77     6  21
53     NA      59  1.7   76     6  22
54     NA      91  4.6   76     6  23
55     NA     250  6.3   76     6  24
56     NA     135  8.0   75     6  25
57     NA     127  8.0   78     6  26
58     NA      47 10.3   73     6  27
59     NA      98 11.5   80     6  28
60     NA      31 14.9   77     6  29
61     NA     138  8.0   83     6  30
62    135     269  4.1   84     7   1
63     49     248  9.2   85     7   2
64     32     236  9.2   81     7   3
65     NA     101 10.9   84     7   4
66     64     175  4.6   83     7   5
67     40     314 10.9   83     7   6
68     77     276  5.1   88     7   7
69     97     267  6.3   92     7   8
70     97     272  5.7   92     7   9
71     85     175  7.4   89     7  10
72     NA     139  8.6   82     7  11
73     10     264 14.3   73     7  12
74     27     175 14.9   81     7  13
75     NA     291 14.9   91     7  14
76      7      48 14.3   80     7  15
77     48     260  6.9   81     7  16
78     35     274 10.3   82     7  17
79     61     285  6.3   84     7  18
80     79     187  5.1   87     7  19
81     63     220 11.5   85     7  20
82     16       7  6.9   74     7  21
83     NA     258  9.7   81     7  22
84     NA     295 11.5   82     7  23
85     80     294  8.6   86     7  24
86    108     223  8.0   85     7  25
87     20      81  8.6   82     7  26
88     52      82 12.0   86     7  27
89     82     213  7.4   88     7  28
90     50     275  7.4   86     7  29
91     64     253  7.4   83     7  30
92     59     254  9.2   81     7  31
93     39      83  6.9   81     8   1
94      9      24 13.8   81     8   2
95     16      77  7.4   82     8   3
96     78      NA  6.9   86     8   4
97     35      NA  7.4   85     8   5
98     66      NA  4.6   87     8   6
99    122     255  4.0   89     8   7
100    89     229 10.3   90     8   8
101   110     207  8.0   90     8   9
102    NA     222  8.6   92     8  10
103    NA     137 11.5   86     8  11
104    44     192 11.5   86     8  12
105    28     273 11.5   82     8  13
106    65     157  9.7   80     8  14
107    NA      64 11.5   79     8  15
108    22      71 10.3   77     8  16
109    59      51  6.3   79     8  17
110    23     115  7.4   76     8  18
111    31     244 10.9   78     8  19
112    44     190 10.3   78     8  20
113    21     259 15.5   77     8  21
114     9      36 14.3   72     8  22
115    NA     255 12.6   75     8  23
116    45     212  9.7   79     8  24
117   168     238  3.4   81     8  25
118    73     215  8.0   86     8  26
119    NA     153  5.7   88     8  27
120    76     203  9.7   97     8  28
121   118     225  2.3   94     8  29
122    84     237  6.3   96     8  30
123    85     188  6.3   94     8  31
124    96     167  6.9   91     9   1
125    78     197  5.1   92     9   2
126    73     183  2.8   93     9   3
127    91     189  4.6   93     9   4
128    47      95  7.4   87     9   5
129    32      92 15.5   84     9   6
130    20     252 10.9   80     9   7
131    23     220 10.3   78     9   8
132    21     230 10.9   75     9   9
133    24     259  9.7   73     9  10
134    44     236 14.9   81     9  11
135    21     259 15.5   76     9  12
136    28     238  6.3   77     9  13
137     9      24 10.9   71     9  14
138    13     112 11.5   71     9  15
139    46     237  6.9   78     9  16
140    18     224 13.8   67     9  17
141    13      27 10.3   76     9  18
142    24     238 10.3   68     9  19
143    16     201  8.0   82     9  20
144    13     238 12.6   64     9  21
145    23      14  9.2   71     9  22
146    36     139 10.3   81     9  23
147     7      49 10.3   69     9  24
148    14      20 16.6   63     9  25
149    30     193  6.9   70     9  26
150    NA     145 13.2   77     9  27
151    14     191 14.3   75     9  28
152    18     131  8.0   76     9  29
153    20     223 11.5   68     9  30

| Not quite! Try again. Or, type info() for more options.

| Type may <- subset(airquality, Month==5) at the prompt.

> may <- subset(airquality, Month==5)

| Your dedication is inspiring!


  |                                                                                   
  |=====================================================                        |  68%
| Now use the R command points to plot May's wind and ozone (in that order) as solid
| blue triangles. You have to set the color and plot character with two separate
| arguments. Note we use points because we're adding to an existing plot.

> plot(airquality$Wind, type="n",airquality$Ozone col = "blue", solid = "traiangles")
Error: unexpected symbol in "plot(airquality$Wind, type="n",airquality$Ozone col"
> plot(airquality, may, col = "blue", solid = "traiangles")
There were 50 or more warnings (use warnings() to see the first 50)

| One more time. You can do it! Or, type info() for more options.

| The code for solid blue trianges is 17 so typing
| points(may$Wind,may$Ozone,col="blue",pch=17) at the prompt should work.

> points(may$Wind,may$Ozone,col="blue",pch=17)

| All that hard work is paying off!


  |                                                                                   
  |======================================================                       |  70%
| Now create the variable notmay by subsetting airquality appropriately.

> subset(airquality)
    Ozone Solar.R Wind Temp Month Day
1      41     190  7.4   67     5   1
2      36     118  8.0   72     5   2
3      12     149 12.6   74     5   3
4      18     313 11.5   62     5   4
5      NA      NA 14.3   56     5   5
6      28      NA 14.9   66     5   6
7      23     299  8.6   65     5   7
8      19      99 13.8   59     5   8
9       8      19 20.1   61     5   9
10     NA     194  8.6   69     5  10
11      7      NA  6.9   74     5  11
12     16     256  9.7   69     5  12
13     11     290  9.2   66     5  13
14     14     274 10.9   68     5  14
15     18      65 13.2   58     5  15
16     14     334 11.5   64     5  16
17     34     307 12.0   66     5  17
18      6      78 18.4   57     5  18
19     30     322 11.5   68     5  19
20     11      44  9.7   62     5  20
21      1       8  9.7   59     5  21
22     11     320 16.6   73     5  22
23      4      25  9.7   61     5  23
24     32      92 12.0   61     5  24
25     NA      66 16.6   57     5  25
26     NA     266 14.9   58     5  26
27     NA      NA  8.0   57     5  27
28     23      13 12.0   67     5  28
29     45     252 14.9   81     5  29
30    115     223  5.7   79     5  30
31     37     279  7.4   76     5  31
32     NA     286  8.6   78     6   1
33     NA     287  9.7   74     6   2
34     NA     242 16.1   67     6   3
35     NA     186  9.2   84     6   4
36     NA     220  8.6   85     6   5
37     NA     264 14.3   79     6   6
38     29     127  9.7   82     6   7
39     NA     273  6.9   87     6   8
40     71     291 13.8   90     6   9
41     39     323 11.5   87     6  10
42     NA     259 10.9   93     6  11
43     NA     250  9.2   92     6  12
44     23     148  8.0   82     6  13
45     NA     332 13.8   80     6  14
46     NA     322 11.5   79     6  15
47     21     191 14.9   77     6  16
48     37     284 20.7   72     6  17
49     20      37  9.2   65     6  18
50     12     120 11.5   73     6  19
51     13     137 10.3   76     6  20
52     NA     150  6.3   77     6  21
53     NA      59  1.7   76     6  22
54     NA      91  4.6   76     6  23
55     NA     250  6.3   76     6  24
56     NA     135  8.0   75     6  25
57     NA     127  8.0   78     6  26
58     NA      47 10.3   73     6  27
59     NA      98 11.5   80     6  28
60     NA      31 14.9   77     6  29
61     NA     138  8.0   83     6  30
62    135     269  4.1   84     7   1
63     49     248  9.2   85     7   2
64     32     236  9.2   81     7   3
65     NA     101 10.9   84     7   4
66     64     175  4.6   83     7   5
67     40     314 10.9   83     7   6
68     77     276  5.1   88     7   7
69     97     267  6.3   92     7   8
70     97     272  5.7   92     7   9
71     85     175  7.4   89     7  10
72     NA     139  8.6   82     7  11
73     10     264 14.3   73     7  12
74     27     175 14.9   81     7  13
75     NA     291 14.9   91     7  14
76      7      48 14.3   80     7  15
77     48     260  6.9   81     7  16
78     35     274 10.3   82     7  17
79     61     285  6.3   84     7  18
80     79     187  5.1   87     7  19
81     63     220 11.5   85     7  20
82     16       7  6.9   74     7  21
83     NA     258  9.7   81     7  22
84     NA     295 11.5   82     7  23
85     80     294  8.6   86     7  24
86    108     223  8.0   85     7  25
87     20      81  8.6   82     7  26
88     52      82 12.0   86     7  27
89     82     213  7.4   88     7  28
90     50     275  7.4   86     7  29
91     64     253  7.4   83     7  30
92     59     254  9.2   81     7  31
93     39      83  6.9   81     8   1
94      9      24 13.8   81     8   2
95     16      77  7.4   82     8   3
96     78      NA  6.9   86     8   4
97     35      NA  7.4   85     8   5
98     66      NA  4.6   87     8   6
99    122     255  4.0   89     8   7
100    89     229 10.3   90     8   8
101   110     207  8.0   90     8   9
102    NA     222  8.6   92     8  10
103    NA     137 11.5   86     8  11
104    44     192 11.5   86     8  12
105    28     273 11.5   82     8  13
106    65     157  9.7   80     8  14
107    NA      64 11.5   79     8  15
108    22      71 10.3   77     8  16
109    59      51  6.3   79     8  17
110    23     115  7.4   76     8  18
111    31     244 10.9   78     8  19
112    44     190 10.3   78     8  20
113    21     259 15.5   77     8  21
114     9      36 14.3   72     8  22
115    NA     255 12.6   75     8  23
116    45     212  9.7   79     8  24
117   168     238  3.4   81     8  25
118    73     215  8.0   86     8  26
119    NA     153  5.7   88     8  27
120    76     203  9.7   97     8  28
121   118     225  2.3   94     8  29
122    84     237  6.3   96     8  30
123    85     188  6.3   94     8  31
124    96     167  6.9   91     9   1
125    78     197  5.1   92     9   2
126    73     183  2.8   93     9   3
127    91     189  4.6   93     9   4
128    47      95  7.4   87     9   5
129    32      92 15.5   84     9   6
130    20     252 10.9   80     9   7
131    23     220 10.3   78     9   8
132    21     230 10.9   75     9   9
133    24     259  9.7   73     9  10
134    44     236 14.9   81     9  11
135    21     259 15.5   76     9  12
136    28     238  6.3   77     9  13
137     9      24 10.9   71     9  14
138    13     112 11.5   71     9  15
139    46     237  6.9   78     9  16
140    18     224 13.8   67     9  17
141    13      27 10.3   76     9  18
142    24     238 10.3   68     9  19
143    16     201  8.0   82     9  20
144    13     238 12.6   64     9  21
145    23      14  9.2   71     9  22
146    36     139 10.3   81     9  23
147     7      49 10.3   69     9  24
148    14      20 16.6   63     9  25
149    30     193  6.9   70     9  26
150    NA     145 13.2   77     9  27
151    14     191 14.3   75     9  28
152    18     131  8.0   76     9  29
153    20     223 11.5   68     9  30

| One more time. You can do it! Or, type info() for more options.

| Type notmay <- subset(airquality, Month!=5) at the prompt.

> notmay <- subset(airquality, Month!=5)

| All that hard work is paying off!


  |                                                                                   
  |=======================================================                      |  71%
| Now use the R command points to plot these notmay's wind and ozone (in that order)
| as red snowflakes.

> points(notmay = wind, ozone, col = "red")
Error in points(notmay = wind, ozone, col = "red") : 
  object 'ozone' not found
> points(notmay = wind, ozone)
Error in points(notmay = wind, ozone) : object 'ozone' not found
> points(notmay, plot(wind, ozone))
Error in plot(wind, ozone) : object 'wind' not found
> points(notmay)

| You're close...I can feel it! Try it again. Or, type info() for more options.

| The code for snowflakes is 8 so typing
| points(notmay$Wind,notmay$Ozone,col="red",pch=8) at the prompt should work.

> points(notmay$Wind,notmay$Ozone,col="red",pch=8)

| Keep working like that and you'll get there!


  |                                                                                   
  |========================================================                     |  73%
| Now we'll use the R command legend to clarify the plot and explain what it means.
| The function has a lot of arguments, but we'll only use 4. The first will be the
| string "topright" to tell R where to put the legend. The remaining 3 arguments will
| each be 2-long vectors created by R's concatenate function, e.g., c(). These
| arguments are pch, col, and legend. The first is the vector (17,8), the second
| ("blue","red"), and the third ("May","Other Months"). Try it now.

> legent("topright", col = ("blue", "red") pch = ("17", "8"), legend("May","Other Months"))
Error: unexpected ',' in "legent("topright", col = ("blue","
> legend("topright", pch = c(17, 8), col = c("blue", "red"), legend = c("May", "Other Months"))

| You are really on a roll!


  |                                                                                   
  |=========================================================                    |  74%
| Now add a vertical line at the median of airquality$Wind. Make it dashed (lty=2)
| with a width of 2.

> abline(median = "airquality$Wind", lty = 2, width = 2)
Warning messages:
1: In int_abline(a = a, b = b, h = h, v = v, untf = untf, ...) :
  "median" is not a graphical parameter
2: In int_abline(a = a, b = b, h = h, v = v, untf = untf, ...) :
  "width" is not a graphical parameter

| You almost had it, but not quite. Try again. Or, type info() for more options.

| Type abline(v=median(airquality$Wind),lty=2,lwd=2).

> abline(v=median(airquality$Wind),lty=2,lwd=2)

| Keep working like that and you'll get there!


  |                                                                                   
  |==========================================================                   |  76%
| Use par with the parameter mfrow set equal to the vector (1,2) to set up the plot
| window for two plots side by side. You won't see a result.

> mfrow(1, 2)
Error in mfrow(1, 2) : could not find function "mfrow"
> plot(mfrow(1,2))
Error in mfrow(1, 2) : could not find function "mfrow"
> par(mfrow = c(1, 2))

| You are doing so well!


  |                                                                                   
  |============================================================                 |  77%
| Now plot airquality$Wind and airquality$Ozone and use main to specify the title
| "Ozone and Wind".

> title(main = "Ozone and Wind")

| Not quite, but you're learning! Try again. Or, type info() for more options.

| Type plot(airquality$Wind, airquality$Ozone, main = "Ozone and Wind").

> plot(airquality$Wind, airquality$Ozone, main = "Ozone and Wind")

| All that practice is paying off!


  |                                                                                   
  |=============================================================                |  79%
| Now for the second plot.

...


  |                                                                                   
  |==============================================================               |  80%
| Plot airquality$Ozone and airquality$Solar.R and use main to specify the title
| "Ozone and Solar Radiation".

> Plot(airquality$Ozone, airquality$Solar.R, main = "Ozone and Solar Radiation")
Error in Plot(airquality$Ozone, airquality$Solar.R, main = "Ozone and Solar Radiation") : 
  could not find function "Plot"
> Plot(airquality$Ozone, airquality$Solar.R)
Error in Plot(airquality$Ozone, airquality$Solar.R) : 
  could not find function "Plot"
> title(main = "Ozone and Solar Radiation")

| You almost had it, but not quite. Try again. Or, type info() for more options.

| Type plot(airquality$Ozone, airquality$Solar.R, main = "Ozone and Solar Radiation").

> plot(airquality$Ozone, airquality$Solar.R, main = "Ozone and Solar Radiation")

| Keep working like that and you'll get there!


  |                                                                                   
  |===============================================================              |  82%
| Now for something more challenging.

...


  |                                                                                   
  |================================================================             |  83%
| This one with 3 plots, to illustrate inner and outer margins. First, set up the plot
| window by typing par(mfrow = c(1, 3), mar = c(4, 4, 2, 1), oma = c(0, 0, 2, 0))

> par(mfrow = c(1, 3), mar = c(4, 4, 2, 1), oma = c(0, 0, 2, 0))

| Perseverance, that's the answer.


  |                                                                                   
  |=================================================================            |  85%
| Margins are specified as 4-long vectors of integers. Each number tells how many
| lines of text to leave at each side. The numbers are assigned clockwise starting at
| the bottom. The default for the inner margin is c(5.1, 4.1, 4.1, 2.1) so you can see
| we reduced each of these so we'll have room for some outer text.

...


  |                                                                                   
  |==================================================================           |  86%
| The first plot should be familiar. Plot airquality$Wind and airquality$Ozone with
| the title (argument main) as "Ozone and Wind".

> title(main = "Ozone and Wind")

| Almost! Try again. Or, type info() for more options.

| Type plot(airquality$Wind, airquality$Ozone, main = "Ozone and Wind").

> plot(airquality$Wind, airquality$Ozone, main = "Ozone and Wind")

| All that practice is paying off!


  |                                                                                   
  |====================================================================         |  88%
| The second plot is similar.

...


  |                                                                                   
  |=====================================================================        |  89%
| Plot airquality$Solar.R and airquality$Ozone with the title (argument main) as
| "Ozone and Solar Radiation".

> plot(airquality$Solar.R, airquality$Ozone, main = "Ozone and Solar Radiation")

| That's a job well done!


  |                                                                                   
  |======================================================================       |  91%
| Now for the final panel.

...


  |                                                                                   
  |=======================================================================      |  92%
| Plot airquality$Temp and airquality$Ozone with the title (argument main) as "Ozone
| and Temperature".

> plot(airquality$Temp, airquality$Ozone, main = "Ozone and Temperature")

| You got it!


  |                                                                                   
  |========================================================================     |  94%
| Now we'll put in a title.

...


  |                                                                                   
  |==========================================================================   |  95%
| Since this is the main title, we specify it with the R command mtext. Call mtext
| with the string "Ozone and Weather in New York City" and the argument outer set
| equal to TRUE.

> mtext(main = "Ozone and Weather in New York City", outer = TRUE)
Error in as.graphicsAnnot(text) : 
  argument "text" is missing, with no default
> title(main = "Ozone and Weather in New York City", outer = TRUE)

| One more time. You can do it! Or, type info() for more options.

| Type mtext("Ozone and Weather in New York City", outer = TRUE).

> mtext("Ozone and Weather in New York City", outer = TRUE)

| That's a job well done!


  |                                                                                   
  |===========================================================================  |  97%
| Voila! Beautiful, right?
