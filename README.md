# gitchecker

The name `gitchecker` is probably bad, but since it's the for metric we wanted
to try out, it's the only thing that occurred to me.

## Running the Project

`pandoc` and `R` are prerequisites and both should be available in `homebrew`,
or your other favorite package manager.

After `R` is installed, the only other dependency is `rmarkdown` in the `R`
console simply do

    $ R
    > install.packages('rmarkdown')

Before you can render `page.Rmd`, you have to change the working directory of
your `R` session

    > setwd('/home/path/to/your/git/project')

Likewise, this has to be set in `page.Rmd`. Right now it is hard wired to
`/home/chris/Projects/any-repository`.

Now you can render `rmarkdown` files with the command

    > render("../gitchecker/page.Rmd")

This results in a `page.html` file that can be opened your browsers.
