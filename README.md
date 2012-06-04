# fontcm

This package contains the Computer Modern font with Paul Murrell's symbol extensions, and is to be used with the **extrafont** package.

The fonts are a subset of the [cm-lgc font package](http://www.ctan.org/tex-archive/help/Catalogue/entries/cm-lgc.html).
The faces with small caps and italics using old-style numerals (which can hang below the baseline) are not included with this package.


# Installation

First, make sure that you have [extrafont](https://github.com/wch/extrafont) installed.

Then, to install `fontcm`:

```R
install_github('fontcm', 'wch')

library(extrafont)
font_install('fontcm')
# In the future, when fontcm is on CRAN, font_install will automatically
# download, install, and then register the font package in the extrafont database
```

You can check to see if they're properly installed:

```R
fonts()
# "CM Roman"               "CM Roman Asian"         "CM Roman CE"
# "CM Roman Cyrillic"      "CM Roman Greek"         "CM Sans"
# "CM Sans Asian"          "CM Sans CE"             "CM Sans Cyrillic"
# "CM Sans Greek"          "CM Symbol"              "CM Typewriter"
# "CM Typewriter Asian"    "CM Typewriter CE"       "CM Typewriter Cyrillic"
# "CM Typewriter Greek"

# For more detailed font information:
fonttable()
```


## Use example

Here is an example of using Computer Modern fonts with math symbols.

```R
library(ggplot2)
library(extrafont)

loadfonts()

pdf('fontcm.pdf', width=4, height=4)

# Base plot
p <- qplot(c(1,5), c(1,5)) +
  xlab("Made with CM fonts") + ylab("Made with CM fonts") +
  opts(title = "Made with CM fonts")

# Equation
eq <- "sum(frac(1, n*'!'), n==0, infinity) == lim(bgroup('(', 1 + frac(1, n), ')')^n, x %->% infinity)"

# Without the new fonts
p + annotate("text", x=3, y=3, parse=TRUE, label=eq)

# With the new fonts
p + annotate("text", x=3, y=3, parse=TRUE, family="CM Roman", label=eq) +
  opts(plot.title = theme_text(size=16, family="CM Roman")) +
  opts(axis.title.x = theme_text(size=16, family="CM Roman", face="italic")) +
  opts(axis.title.y = theme_text(size=16, family="CM Sans", face="bold", angle=90))

dev.off()

# Embed the fonts
embed_fonts('fontcm.pdf', outfile='fontcm-embed.pdf')
```
