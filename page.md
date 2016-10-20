


```r
library(rmarkdown)
blub <- sample(1:100, 1)
```


```r
setwd("/home/chris/Projects/ham-app/")
rawData <- read.table(text =system('git log --pretty=tformat: --numstat | cut -f 1,2', intern = T), stringsAsFactors=FALSE)
str(rawData)
```

```
## 'data.frame':	2210 obs. of  2 variables:
##  $ V1: chr  "1" "1" "14" "3" ...
##  $ V2: chr  "1" "1" "0" "3" ...
```

```r
toNA <- function(x) {
  if(identical("-", x)) {
    NA
  } else {
    x
  }
}

polishedData <- rawData
polishedData <- data.frame(lapply(polishedData, toNA), stringsAsFactors = FALSE)

polishedData$V1 <- as.numeric(rawData$V1)
```

```
## Warning: NAs introduced by coercion
```

```r
polishedData$V2 <- as.numeric(rawData$V2)
```

```
## Warning: NAs introduced by coercion
```

```r
polishedData$linesAdded <- as.numeric(rawData$V1)
```

```
## Warning: NAs introduced by coercion
```

```r
polishedData$linesSubtracted <- as.numeric(rawData$V2)
```

```
## Warning: NAs introduced by coercion
```

```r
polishedData <- polishedData[complete.cases(polishedData),]

meanLinesAdded = mean(polishedData$linesAdded)
meanLinesSubtracted = mean(polishedData$linesSubtracted)
meanGrowth = meanLinesAdded - meanLinesSubtracted

index <- sample(1:nrow(polishedData), 1)
randomRow <- polishedData[index,]
addedLinesForRow = randomRow$linesAdded - randomRow$linesSubtracted
```

## script should be here

<script>
  window.onload = function () {
      var s = Snap("#blobb");

      var shadow = s.ellipse(250,550,150,10);
      var growthFactor = 0;

      var meanGrowth = 10.5382803;
      var addedLinesForRow = 43;
      console.log("addedLinesForRow: ", addedLinesForRow);
      console.log("index: ", 320);
      console.log("meanGrowth: ", 10.5382803);
      if(addedLinesForRow > 5*meanGrowth) {
        growthFactor = 100;
      } else if ( addedLinesForRow > 2 * meanGrowth) {
        growthFactor = 50;
      }

      var bunnybody = s.path("M150 0,L150 300, 200 450, 250 500, 300 450, 350 300, 350 0, 250 200");

      var leftEye = s.circle(200,300,15);

      var rightEye = s.circle(300,300,15);

      bunnybody.attr({
          fill: "#fff",
          stroke: "#fff"
      });

      shadow.attr({
          fill: "#666"
      });

      leftEye.attr({
          fill: "#000",
          stroke: "#fff"
      });

      rightEye.attr({
          fill: "#000",
          stroke: "#fff"
      });

      bunnybody.animate({d: "M150 0, L" + (150 - growthFactor) + " 300, " + (200 - growthFactor) + " 450, 250 500, " + (300 + growthFactor) + " 450, " + (350 + growthFactor) + " 300, 350 0, 250 200"}, 1000);
      rightEye.animate({ x: 80, y: 10, r: 30 }, 1000);
      leftEye.animate({ r: "10" }, 1000);

  };

</script>

<svg id="blobb"></svg>
