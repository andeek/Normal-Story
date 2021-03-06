One Curve to Rule Them All...
========================================================
###By Omesh Johar, Lindsey Jackson, and Andee Kaplan

It began with the forging of the Curves of Normal. Three were given to the Elves; immortal, wisest and fairest of all beings.

```r
library(ggplot2)
library(reshape2)
library(RColorBrewer)

mu <- c(2, 3, 4)
sigma <- (0.15)

df.e <- data.frame(x = seq(0, 6, by = 0.01))
df.e <- cbind(df.e, sapply(mu, function(m) dnorm(df.e$x, m, sigma)))
df.e.m <- melt(df.e, id.vars = "x")

brew.e <- brewer.pal(5, "Greens")[-(1:2)]

qplot(x, 0.25 * value, group = variable, colour = variable, data = df.e.m, geom = "line") + 
    ylim(c(0, 1)) + xlab("") + ylab("") + guides(colour = FALSE) + ggtitle("Curves given to the Elves") + 
    scale_colour_manual(values = brew.e) + theme_bw() + theme(axis.ticks = element_blank(), 
    axis.line = element_blank(), axis.text.x = element_blank(), axis.text.y = element_blank(), 
    axis.ticks = element_blank(), axis.title.x = element_blank(), axis.title.y = element_blank(), 
    panel.border = element_blank(), panel.grid.major = element_blank(), panel.grid.minor = element_blank())
```

![plot of chunk unnamed-chunk-1](figure/unnamed-chunk-1.png) 

```r

```


Seven, to the Dwarf Lords, great data miners and graphsmen of the mountain halls. 


```r
mu <- 1:7 * 5
sigma <- (5)

df.d <- data.frame(x = seq(min(mu) - 3 * sigma, max(mu) + 3 * sigma, by = 0.01))
df.d <- cbind(df.d, sapply(mu, function(m) dnorm(df.d$x, m, sigma)))
df.d.m <- melt(df.d, id.vars = "x")

brew.d <- brewer.pal(9, "YlOrBr")[-(1:2)]

qplot(x, value, group = variable, colour = variable, data = df.d.m, geom = "line") + 
    ylim(c(0, 1)) + xlab("") + ylab("") + guides(colour = FALSE) + ggtitle("Curves given to the Dwarves") + 
    scale_colour_manual(values = brew.d) + theme_bw() + theme(axis.ticks = element_blank(), 
    axis.line = element_blank(), axis.text.x = element_blank(), axis.text.y = element_blank(), 
    axis.ticks = element_blank(), axis.title.x = element_blank(), axis.title.y = element_blank(), 
    panel.border = element_blank(), panel.grid.major = element_blank(), panel.grid.minor = element_blank())
```

![plot of chunk unnamed-chunk-2](figure/unnamed-chunk-2.png) 

```r

```


And nine--nine curves were gifted to the race of Men, who above all else desire power. For within these curves was bound the strength and the will to govern over each race. 


```r
mu <- 1:9 * 7
sigma <- (2)

df.m <- data.frame(x = seq(min(mu) - 3 * sigma, max(mu) + 3 * sigma, by = 0.01))
df.m <- cbind(df.m, sapply(mu, function(m) dnorm(df.m$x, m, sigma)))
df.m.m <- melt(df.m, id.vars = "x")

brew.m <- brewer.pal(9, "Purples")

qplot(x, 4 * value, group = variable, colour = variable, data = df.m.m, geom = "line", 
    size = 3) + ylim(c(0, 1)) + xlab("") + ylab("") + guides(colour = FALSE, 
    size = FALSE) + ggtitle("Curves given to the Race of Men") + scale_colour_manual(values = brew.m) + 
    theme_bw() + theme(axis.ticks = element_blank(), axis.line = element_blank(), 
    axis.text.x = element_blank(), axis.text.y = element_blank(), axis.ticks = element_blank(), 
    axis.title.x = element_blank(), axis.title.y = element_blank(), panel.border = element_blank(), 
    panel.grid.major = element_blank(), panel.grid.minor = element_blank())
```

![plot of chunk unnamed-chunk-3](figure/unnamed-chunk-3.png) 


But they were all of them deceived, for a new curve was made. In the land of Moivre-dor, in the fires of **M o $\mu$ n t <sp></sp>D $\sigma\sigma$ m**, the Dark Lord Gausson forged in secret, a standard Normal curve, to control all others. And into this master curve he poured all his cruelty, his malice and his will to dominate all life. One curve to rule them all. 


```r
# install.packages('jpeg')
library(jpeg)
library(grid)
img <- readJPEG("ring-lord-of-the-rings.jpg")
g <- rasterGrob(img, interpolate = TRUE)

x <- seq(-3, 3, by = 0.01)
qplot(x, dnorm(x), geom = "blank") + annotation_custom(g, xmin = -Inf, xmax = Inf, 
    ymin = -Inf, ymax = Inf) + geom_area(fill = "red", alpha = 0.6) + xlab("") + 
    ylab("") + ggtitle("...And in the Darkness Bind them.") + theme_bw() + theme(axis.ticks = element_blank(), 
    axis.line = element_blank(), axis.text.x = element_blank(), axis.text.y = element_blank(), 
    axis.ticks = element_blank(), axis.title.x = element_blank(), axis.title.y = element_blank(), 
    panel.border = element_blank(), panel.grid.major = element_blank(), panel.grid.minor = element_blank())
```

![plot of chunk unnamed-chunk-4](figure/unnamed-chunk-4.png) 


One by one, the free peoples of Middle-earth fell to the power of the Curve. But there were some who resisted. A last alliance of men and elves marched against the armies of Moivre-dor, and on the very slopes of  **M o $\mu$ n t <sp></sp>D $\sigma\sigma$ m**, they fought for the freedom of Middle-earth. 


```r
pars <- data.frame(mu = c(1:19 * 3 + 20, 0), sigma = c(rep(0.15, 3), rep(5, 
    7), rep(2, 9), 1), mult = c(rep(0.1, 3), rep(1, 7), rep(1, 9), 2))

df <- with(pars, data.frame(x = seq(min(mu) - 3 * max(sigma), max(mu) + 3 * 
    max(sigma), by = 0.01)))
df <- cbind(df, apply(pars, 1, function(m) m["mult"] * dnorm(df$x, m["mu"], 
    m["sigma"])))
df.me <- melt(df, id.vars = "x")

brew <- c(brew.e, brew.d, brew.m, "red")

qplot(x, value, group = variable, colour = variable, data = df.me, geom = "line") + 
    xlab("") + ylab("") + guides(colour = FALSE, size = FALSE) + ggtitle("An alliance of Middle Earth marching against the One Curve") + 
    scale_colour_manual(values = brew) + theme_bw() + theme(axis.ticks = element_blank(), 
    axis.line = element_blank(), axis.text.x = element_blank(), axis.text.y = element_blank(), 
    axis.ticks = element_blank(), axis.title.x = element_blank(), axis.title.y = element_blank(), 
    panel.border = element_blank(), panel.grid.major = element_blank(), panel.grid.minor = element_blank())
```

![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-5.png) 


Victory was near, but the power of the Curve could not be undone. It was in this moment, when all hope had faded, that Sir Isaac Newton, son of the king, took up his father's gravity. And Gausson, enemy of the free peoples of Middle-earth, was defeated. The Curve passed to Sir Isaac Newton...


```r
img <- readJPEG("sir-isaac-newton.jpg")
g <- rasterGrob(img, interpolate = TRUE)

x <- seq(-3, 3, by = 0.01)
qplot(x, dnorm(x), geom = "blank") + annotation_custom(g, xmin = -Inf, xmax = Inf, 
    ymin = -Inf, ymax = Inf) + geom_area(fill = "red", alpha = 0.6) + xlab("") + 
    ylab("") + ggtitle("...The Curve passed to") + theme_bw() + theme(axis.ticks = element_blank(), 
    axis.line = element_blank(), axis.text.x = element_blank(), axis.text.y = element_blank(), 
    axis.ticks = element_blank(), axis.title.x = element_blank(), axis.title.y = element_blank(), 
    panel.border = element_blank(), panel.grid.major = element_blank(), panel.grid.minor = element_blank())
```

![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6.png) 


...who had this one chance to destroy evil forever, but the hearts of men are easily corrupted. And the curve of power has a will of its own. It betrayed Sir Isaac Newton, to his death. And some things that should not have been forgotten were lost. History became legend. Legend became myth. And for two and a half thousand years, the Curve passed out of all knowledge. Until, when chance came, the Curve ensnared every introductory Statistics student in Middle Earth. 

