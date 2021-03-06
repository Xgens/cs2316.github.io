# CS 2316 Data Manipulation

This repository contains the [Jekyll](http://jekyllrb.com/) source of the public web site for [Chris Simpkins](https://github.com/csimpkins)'s sections of CS 2316 at Georgia Tech.

## Running the Site locally

I used to include GitHub's Gemfile so that we could run the site locally using [GitHub's instructions](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/), but GitHub insists on using that awful piece of garbage Nokogiri which means to run GitHub pages locally you'll need to lose hours of your life randomly every few months solving installation problems. I'm not a Ruby dev expert and I don't want to become one just so I can run GitHub Pages locally. So I removed GitHub's Gemfile and you can just run the site locally like you would any other Jekyll site:

```sh
jekyll serve
```

and visit [http://localhost:4000](http://localhost:4000) in your browser. Some minor Markdown rendering details may differ from GitHub when running locally.

## Compiling the Slides

Some slides are written in Markdown and converted to Reveal.js HTML using [Pandoc](http://pandoc.org/) to  [produce the slides](http://pandoc.org/README.html#producing-slide-shows-with-pandoc)

```sh
$ cd slides
$ pandoc -s --mathjax -t revealjs -V theme=gt -V "slideNumber='c/t'" -V progress=true -o intro-python.html intro-python.md

```

To generate all the slides:

```sh
for file in `ls *.md`; do pandoc -s --mathjax -t revealjs -V theme=gt -V "slideNumber='c/t'" -V progress=true -o $(basename $file .md).html $file; done
```

I'm gradually moving to PDF slides generated from [org-mode](http://orgmode.org/) sources using the [beamer exporter](http://orgmode.org/worg/exporters/beamer/tutorial.html). Students seem to prefer having printable copies (and the print CSS from Reveal.js doesn't always produce nice results), I like not having upstream changes to Reveal.js and Mathjax suddenly break my slides, and using org-mode gives me succinct source syntax like Markdown with the power of LaTeX/Beamer. Go [Emacs](https://www.gnu.org/software/emacs/)!

## Generating the Schedule

I use my own [course tools](https://github.com/csimpkins/course-tools) to generate the schedule each semester. At the beginning of the semester, create a file containing the breaks. For example, `summer2017-breaks.json` (note that all dates are in [ISO 8601](https://xkcd.com/1179/) format):

```js
{
    "2017-05-29": "Memorial Day",
    "2017-07-03": "Independence Day Break",
    "2017-07-04": "Independence Day Break"
}
```

Then run `make_schedule.py` to generate a starter schedule like this:

```sh
make_schedule.py -f 2017-05-15 -l 2017-07-25 -d TR -b summer2017-breaks.json -c cs2316.json -o cs2316.summer2017
```

This will create a file named `cs2316.summer2017` with contents like:

```
Week 1
2017-05-16;intro-cs2316
2017-05-18;intro-python
Week 2
2017-05-23;values-variables
2017-05-25;data-structures
```

You'll need to customize this file, especially for summer semesters. For the rest of the semester, you'll update the schedule by modifying this file and running `render_schedule.py`. Before running `render_schedule.py` make an HTML template file for the semester schedule with a `.jinja2` extension, e.g., `summer2017.html.jinja2`.  The easiest way is to copy the previous semester's template file and modify the schedule information at the top for the current semester. Run `render_schedule.py` like this:

```sh
render_schedule.py -s cs2316.summer2017 -c cs2316.json -t summer2017.html.jinja2 -o summer2017.html
```

which creates the `summer2017.html` file. (Remember to update the redirect in [`schedule.html`](schedule.html) to point to the new file at the beginning of the semester.)

If you wish, you can use a custom course materials file instead of [`cs2316.json`](cs2316.json).

### Adding Materials and Reminders

To add materials, edit the schedule file, e.g., [`cs2316.summer2017`](cs2316.summer2017) and add text to the third field. For example (note that fields are separated with semicolons, items within fields are separated with commas):

```
Week 1
2017-05-16;intro-cs2316,intro-java, values-variables;[T-Square Site](https://t-square.gatech.edu/portal/site/gtc-b435-1ace-5039-bb99-451228e2b767)
2017-05-18;control-structures, data-structures
```

To add reminders, such as homework links, add text to the fourth field. Note that if the third field is empty, you'll have what appears to be an extra `;`. For example (note the line for 2017-05-23):

```
Week 1
2017-05-16;intro-cs2316,intro-java, values-variables; [T-Square Site](https://t-square.gatech.edu/portal/site/gtc-b435-1ace-5039-bb99-451228e2b767);[HW0 Assigned](summer2017/hw0/hw0.html)
2017-05-18;control-structures, data-structures
Week 2
2017-05-23;arrays;;[HW0 Due](summer2017/hw0/hw0.html)
2017-05-25;data-abstraction, classes
```

Note you can make links using the Markdown `[link text](link target)` syntax.

Be sure to commit any changes to the schedule file, schedule template, and schedule to the repo.

## Slides

Some slides are HTML Reveal.js slides produced from Markdown sources. Source files use a `.md` ending. We use [Pandoc](http://pandoc.org/) to  [produce the slides](http://pandoc.org/README.html#producing-slide-shows-with-pandoc)

To recompile all slides:

```sh
cd slides
for file in `ls *.md`; do pandoc -s --mathjax -t revealjs -V theme=gt -V "slideNumber='c/t'" -V progress=true -o $(basename $file .md).html $file; done
```

Some slides are PDFs produced from LaTeX Beamer sources. Source files use a `.tex` ending.

As of Fall 2016 I'm moving to PDF slides produced from org-mode sources (with a `.org` ending). Students seem to prefer having printable copies (and the print CSS from Reveal.js doesn't always produce nice results), I like not having upstream changes to Reveal.js and Mathjax suddenly break my slides, and using org-mode gives me succinct source syntax like Markdown with the power of LaTeX/Beamer. Go Emacs!