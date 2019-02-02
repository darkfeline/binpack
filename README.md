# binpack

Command binpack is a Go generator for packing static assets into Go
packages.

For example, if you have file base.html in your package containing:

    <html><body>{{.body}}</body></html>

You can add a generate line anywhere in your package:

    //go:generate binpack -var myTemplate base.html

Then running go generate will produce a myTemplate_packed.go containing:

    // Code generated by "binpack -var myTemplate base.html"; DO NOT EDIT.

    package foo

    var myTemplate = "<html><body>{{.body}}</body></html>"

This also works for binary files, although the generated source is
very inefficient as it is encoded as a string literal (but after
compiling the data should not take up any extra space).
