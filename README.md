# csasdown <img src='man/figures/csasdown-logo.png' align="right" height="139" />

> Reproducible CSAS Reports with R Markdown

<!-- badges: start -->
[![R-CMD-check](https://github.com/pbs-assess/csasdown/workflows/R-CMD-check/badge.svg)](https://github.com/pbs-assess/csasdown/actions)
<!-- badges: end -->

<!-- [![Coverage status](https://codecov.io/gh/pbs-assess/csasdown/branch/master/graph/badge.svg)](https://codecov.io/github/pbs-assess/csasdown?branch=master) -->

csasdown is an R package that facilitates generating Canadian Science Advisory Secretariat (CSAS) documents in PDF or Word format using R Markdown and bookdown.

Please check the [wiki](https://github.com/pbs-assess/csasdown/wiki) for hints and FAQs.

Slides from a short workshop on csasdown: [[PDF](https://www.dropbox.com/s/7m23mh3yfhk5ah8/csasdown-slides.pdf?dl=1)].

Have a problem? If it's a bug or feature request please post it as a [GitHub Issue](https://github.com/pbs-assess/csasdown/issues). If it's a quick question on csasdown use, find us on [DFO MS Teams](https://teams.microsoft.com/l/channel/19%3ae15d7a8e776b418b8e4975a4c9c5f93f%40thread.skype/R%2520-%2520csasdown?groupId=50a32c0d-d5fe-4368-b95b-4beaaa1ba1a1&tenantId=1594fdae-a1d9-4405-915d-011467234338).

**If you use csasdown to write a report, please let us know so we can add it to the list of publications using the package. This helps us justify spending our work time on its development. You can post an issue, make a pull request adding it to this readme, send us a quick email (contact details [here](https://github.com/pbs-assess/csasdown/blob/c76731e8580bb12da9324e56ff5e56a8d4901aeb/DESCRIPTION#L5-L8)), or find us on [DFO MS Teams](https://teams.microsoft.com/l/channel/19%3ae15d7a8e776b418b8e4975a4c9c5f93f%40thread.skype/R%2520-%2520csasdown?groupId=50a32c0d-d5fe-4368-b95b-4beaaa1ba1a1&tenantId=1594fdae-a1d9-4405-915d-011467234338).**

## Initial setup

To compile PDF documents using R, you need to have Pandoc, LaTeX, and several related packages installed. If you have a recent version of  [RStudio](http://www.rstudio.com/products/rstudio/download/), then you already have Pandoc.

1. You will need to install LaTeX if you do not have it already. Read [this Wiki page](https://github.com/pbs-assess/csasdown/wiki/Latex-Installation-for-csasdown) for a detailed description of this procedure. Most likely you will want to use the R package tinytex.

2. Install the csasdown package:

```r
install.packages("remotes")
remotes::install_github("pbs-assess/csasdown")
```

3. Create a new project in a new directory to hold your document project and all the files that csasdown creates. If you're using RStudio: click File -> New Project -> New Directory -> New Project, then type the name of the project in the **Directory name** box. Check the box **Open in new session**. If you are going to use GitHub version control (or if you are not sure), check the box **Create a git repository**. Click **Create Project**. A new RStudio project will open up, and will have its working directory set to the new document project's directory.

4. Run this line in your R console to create a new Research Document from the built-in template in whatever your working directory is:

```r
csasdown::draft("resdoc")
```

You can do the same for a Technical Report:

```r
csasdown::draft("techreport")
```

or for a Science Response:

```r
csasdown::draft("sr")
```

Note that the `techreport` example contains a lot of information on getting started with R Markdown and should be the first one you render if you are new to `csasdown`. The `resdoc` example contains other examples.

5. Render the document right away to make sure everything works by opening the file **index.Rmd** and clicking the **knit** button in RStudio. Once completed, a preview pane showing the PDF document will appear. The location of the PDF is in the **_book** directory. See the *Rendering* section below for more information.

6. Read the output PDF carefully and compare with what is written in the .Rmd files. This will help you understand more quickly how the document is put together and how you might want to structure your document.

7. *(Optional but recommended)* Create a blank repository on GitHub, commit your changes, and push to GitHub. New to Git? Start with <https://happygitwithr.com/>.

<!--
Open your git client software, navigate to the working directory of your new project and type the following commands:

```git add *``` to add all the new files you created in step 4.

```git commit -m "Initial commit"```

```git remote add origin URL``` where URL is the new repository URL as copied from the GitHub site.

```git remote -v``` verifies you entered the correct URL and it is bound to **origin**

```git push --set-upstream origin master```

Look on your GitHub repository and you should see all the new files there. Your git client is now set up to push and fetch from your repository on GitHub.
-->

8. Need to make an English *and* French version? csasdown has support for both. Also see csasdown's sister package [rosettafish](https://github.com/pbs-assess/rosettafish).

## Publications prepared using csasdown

A list of the publications can be found on this [wiki page](https://github.com/pbs-assess/csasdown/wiki/Publications-prepared-using-csasdown).

## Day-to-day writing

You need to edit the individual chapter R Markdown files to write your report. While writing, you should `git commit` your work frequently. For a gentle novice-friendly guide to getting starting with using Git with R and RStudio, see <http://happygitwithr.com/>.

## Rendering

***
**Render the document often!**

This can't be stressed enough. Every time you add something new, render the document to make sure you didn't break the build. It is much easier to find the problem when only one small known change was made since the last time it was rendered. 
***

To render your report into a PDF or Word document, open `index.Rmd` in RStudio and then click the "knit" button:

<img src="screenshots/knit.png" width="400">

To change the output formats between PDF and Word look at the YAML header part of `index.Rmd`  (the part between the two sets of triple dashes) and change this:

```
output:
 csasdown::resdoc_pdf:
   french: false
```

to this:

```
output:
 csasdown::resdoc_word:
   french: false
```

**Notes**
* This is also the only place you should be changing your document language.
* Replace `resdoc_pdf` and `resdoc_word` with `sr_pdf`, `sr_word`, `techreport_pdf`, or `techreport_word` for other document types.

Alternatively, if you're not using RStudio, you can run this from the R console, assuming your have set the main directory (the one with the `index.Rmd` file) as your working directory:

```r
csasdown::render("index.Rmd")
```

This method of rendering also allows you to insert `browser()` calls in your code and stop compilation to debug (but note you'll need to run `sink()` in the console if you stop mid R Markdown rendering in a `browser()`). It also does *not* open a preview viewer once finished, so you will have to navigate to the `_book/` directory and open it up manually.

The rendered PDF or Word file of your report will be deposited in the `_book/` directory.

<img src="screenshots/example-titlepage.png" width="450">

<img src="screenshots/example-page.png" width="450">

<!--
If you want to add a CSAS-formatted .docx title page to a Res Doc, edit the file `templates/RES2016-eng-titlepage.docx` as desired and run the command:

```r
csasdown::add_resdoc_docx_titlepage()
```

This will attach the title page to the beginning of the Word document.
-->

## Components

The following components are ones you should edit to customize your report:

### `_bookdown.yml`

This is the main configuration file for your report. It determines what `.Rmd` files are included in the output, and in what order. Arrange the order of your chapters in this file and ensure that the names match the names in your folders. If you add new `.Rmd` files, add them here. You may comment out some files while working on others by placing a `#` in front of them. This will stop compilation of those files, reducing the time to compile while working on another file.

### `index.Rmd`

This file contains all the meta information that goes at the beginning of your document. You'll need to edit this to put your name on the first page, add the title of your report, etc. **The name of this file cannot be changed.**

### `01-chap1.Rmd`, `02-chap2.Rmd`, etc.

These are the .Rmd files for each chapter/section of your report. Write your report in these. You can delete any or all of these and create as many of your own as you wish, but if you do you must change the **_bookdown.yml** file accordingly.

### `bib/`

Store your bibliography (as BibTeX files) here. You might look at the [citr addin](https://github.com/crsh/citr) and [Zotero](https://www.zotero.org/) to efficiently manage and insert citations.

### `csl/`

Style files for bibliographies should be stored here. You will want to use the included `csas.csl`, which is based on the CJFAS (Canadian Journal of Fisheries and Aquatic Sciences) `.csl` file.

### `figure/` and `data/`

Store pre-made figures and data here and reference them in your R Markdown files. See the [bookdown book](https://bookdown.org/yihui/bookdown/) for details on cross-referencing items using R Markdown.

### `templates/`

This contains any `.docx` or `.tex` files that are need to compile the documents. With the exception of the title page file, you shouldn't have to edit any of these files.

## Related projects

This project has drawn directly on code and ideas from the following:

- <https://github.com/benmarwick/huskydown>
- <https://github.com/ismayc/thesisdown>

[NAFOdown](https://github.com/nafc-assess/NAFOdown) is a derivative of csasdown for rendering NAFO (Northwest Atlantic Fisheries Organization) reports.

## Contributing

If you would like to contribute to this project, please start by reading our [Guide to Contributing](CONTRIBUTING.md). Please note that this project is released with a [Contributor Code of Conduct](CONDUCT.md). By participating in this project you agree to abide by its terms.
