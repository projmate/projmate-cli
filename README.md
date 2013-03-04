# projmate-cli

Projmate is a declarative and more intuitive project system

* Build environments are first class citizens
* Uses pipe and filters instead of everything-is-task hammer
* Watch is built into every task

This is the CLI. The sexy drag 'n drop GUI to follow.

## Installation

To install

    npm install projmate-cli -g

## Example Projfile.coffee

```coffeescript

exports.project = (pm) ->
  f = pm.filters()

  pm.registerTasks
    stylesheets:
      _desc: "Builds all stylesheets"
      _files:
        include: [
          "client/css/barclet.less"
          "client/css/style.less"
          "client/css/styleEmbedded.less"
          "client/css/styleInline.less"
        ]
        # Watch all less files not just the main ones for rebuilding.
        watch: [
          "client/css/**/*.less"
        ]

      development: [
        f.less(dumpLineNumbers: "comments")
        f.addHeader(text: "/* Stylesheets are belong to us! */")
        f.writeFile(lchomp: "client", destinationDir: "build")
      ]

      production: [
        f.less(dumpLineNumbers: "comments")
        f.addHeader(text: "/* Stylesheets are belong to us! */")
        f.cssMinify
        f.gzip
        f.writeFile(lchomp: "client", destinationDir: "build")
      ]
```

## License

Copyright (c) 2013 Mario Gutierrez <mario@projmate.com>

See the file LICENSE for copying permission.

