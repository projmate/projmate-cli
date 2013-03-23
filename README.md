# projmate-cli

Projmate takes the best of Jake, Grunt and my experience with project
deployments.

* Build environments are first class citizens
* Uses pipe and filters instead of everything-is-a-task hammer
* Watch is built into every task
* HTTP and HTTPS server for testing non-secure connections

## Installation

To install

    npm install projmate-cli@0.1.0-dev -g

## Example Projfile.coffee

```coffeescript

exports.project = (pm) ->
  f = pm.filters()
  $ = pm.shell()

  pm.registerTasks
    stylesheets:
      desc: "Builds all stylesheets"
      files:
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

