This is the MIT-licensed tooling of Bob Nystrom's "[Crafting Interpreters][]"
project. It can be used to write minimalist blogs or whole books.

[crafting interpreters]: http://craftinginterpreters.com

## License

[Bob's upstream project][] is double-licensed. It uses MIT for the tooling and
CC BY-NC-ND 4.0 for the "content files" (the text files, the SCSS styling,
and so on). This project stripped all of those content files and left only
the tooling and the scaffold.

[Bob's upstream project]: https://github.com/munificent/craftinginterpreters

Feel free to fork this, and add your own content.

## Build

### Prerequisites

* POSIX environment
* [Dart][] SDK installed

[dart]: https://dart.dev/

Run the following once.

```sh
$ make get
```

This downloads all the packages used by the scripts in `/tools`.

### Writing

Bob:

> The Markdown and snippets of source code are woven together into the final
HTML using a hand-written static site generator that started out as a [single 
tiny Python script][py] for [my first book][gpp] and somehow grew into 
something approximating a real program.

[py]: https://github.com/munificent/game-programming-patterns/blob/master/script/format.py
[gpp]: http://gameprogrammingpatterns.com/

> The generated HTML is committed in the repo under `site/`. It is built from a
combination of Markdown for prose, which lives in `book/`, and snippets of code
that are weaved in from the Java and C implementations in `java/` and `c/`. (All
of those funny looking comments in the source code are how it knows which
snippet goes where.)

> The script that does all the magic is `tool/bin/build.dart`. You can run that
directly, or run:

> ```sh
> $ make book
> ```

> That generates the entire site in one batch. If you are incrementally working
on it, you'll want to run the development server:

> ```sh
> $ make serve
> ```

> This runs a little HTTP server on localhost rooted at the `site/` directory.
Any time you request a page, it regenerates any files whose sources have been
changed, including Markdown files, interpreter source files, templates, and
assets. Just let that keep running, edit files locally, and refresh your
browser to see the changes.

## Repository Layout

*   `asset/` – Sass files and mustache templates used to generate the site.
*   `book/` - Markdown files for the text of each chapter.
*   `build/` - Intermediate files and other build output (except for the site
    itself) go here. Not committed to Git.
*   `site/` – The final generated site. The contents of this directory directly
    mirror the output of `build.dart`. Most content here is generated by this
    script, but fonts, images, and JS only live here. Everything is committed,
    even the generated content.
*   `tool/` – Dart package containing the build, test, and other scripts.

## Useful hints

To convert from HTML to Markdown using `pandoc`, do this:

```sh
pandoc -i some_file.html -o book/final-article-name.md 
```
