tooltipsterR
============

> Interactive Tooltip htmlwidget

[![Linux Build
Status](https://travis-ci.org//tooltipsterR.svg?branch=master)](https://travis-ci.org//tooltipsterR)
[![](http://www.r-pkg.org/badges/version/tooltipsterR)](http://www.r-pkg.org/pkg/tooltipsterR)
[![CRAN RStudio mirror
downloads](http://cranlogs.r-pkg.org/badges/tooltipsterR)](http://www.r-pkg.org/pkg/tooltipsterR)

`tooltipsterR` is an htmlwidget wrapper for the excellent jQuery
[tooltipster](iamceege.github.io/tooltipster/) library for interactive
tooltips.

Installation
------------

    devtools::install_github("timelyportfolio/tooltipsterR")

Usage
-----

### Basic with `htmltools`

    library(tooltipsterR)
    library(htmltools)

    browsable(
      tagList(
        tags$p(
          "See my ",
          tags$span(
            class="tooltip",
            style="color:gray;",
            title="tooltips provided by tooltipsterR",
            "tooltip"
          )
        ),
        tooltipster()
      )
    )

### Medium with `formattable`

    library(tooltipsterR)
    library(formattable)
    library(htmltools)

    #example from ?formatter
    top10red <- formatter(
      "span",
      class = x ~ ifelse(rank(-x) <= 10, "tooltipster-tooltip", ""),
      style = x ~ ifelse(rank(-x) <= 10, "color:red", NA),
      title = x ~ ifelse(rank(-x) <= 10, "top 10", "not top 10")
    )
    yesno <- function(x) ifelse(x, "yes", "no")

    browsable(
      tagList(
        formattable::as.htmlwidget(formattable(mtcars, list(mpg = top10red, qsec = top10red, am = yesno))),
        tooltipster(".tooltipster-tooltip")
      )
    )

### Medium with `remoji`

    library(tooltipsterR)
    library(remoji)
    library(stringi)
    library(htmltools)

    browsable(
      tagList(
        twemoji(),
        lapply(
          find_emoji(""),
          function(heart){
            tags$div(
              style="float:left;",
              class="tooltip",
              title = heart,
              HTML(stri_trans_general(emoji(heart),"any-hex/xml"))
            )
          }
        ),
        tooltipster()
      )
    )

### Advanced with `svglite`

    library(tooltipsterR)
    library(htmltools)
    library(svglite)

    browsable(
      tagList(
        htmlSVG(plot(1:3,col=blues9[7:9],pch=16)),
        tooltipster(),
        tags$script(
    "
    $('circle').each(function(){
      $(this).tooltipster({
        content: $(this).css('fill')
      })
    })
    "      
        )
      )
    )

License
-------

MIT + file LICENSE © [Kenton Russell](https://github.com/).
