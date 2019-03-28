# HTML Packaging

### The problem

Conside this example from [/sample/original/index.html](/sample/original/index.html)

```markup
<!-- /sample/original/index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Hello world</title>
    <link rel="stylesheet" href="assets/style.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.3.1/jquery.js"></script>
</head>
<body>
    <div class="content">
        <img src="https://ichef.bbci.co.uk/news/660/cpsprodpb/71E1/production/_99735192_gettyimages-459467912.jpg" alt="A permanent cat picture">
        <p>Q: Why is this cat so grumpy?</p>
        <p>A: Nobody knows.</p>
    </div>
</body>
</html>
```

Here we have a page with 3 external assets.

```markup
<link rel="stylesheet" href="assets/style.css">
```

This references will simply _not_ work when deployed, as your page will get a URL like `arweave.net/your-tx-id`. As the Arweave data API is flat you we can't have an `assets` directory, and we can't have a named file. All data on the Arweave network gets pseudorandom ID and address like `arweave.net/hNvBcEOgEpeFTnYyLYayaU1h6jgG1KSl5Ujvab2js8Q`. You could upload your CSS first, then your HTML and use the CSS file transaction ID as the `href` like `<link rel="stylesheet" href="your-css-trasnaction-id">` but that's a lot of work.

```markup
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.3.1/jquery.js"></script>

<img src="https://ichef.bbci.co.uk/news/660/cpsprodpb/71E1/production/_99735192_gettyimages-459467912.jpg" alt="A permanent and grumpy cat">
```

These two lines wil work... _for now_. If the BBC change their image URLs or remove the linked image it's now gone forever, any Arweave pages that refernced it will now have a blank space where that image was. The same issue exists for the cloudflare jQuery reference, so _at some point_ this Arweave page will stop working correctly. Maybe it's tomorrow, maybe it's 10 years.

### The solution

We can use the `--package` flag to avoid all of this. It works by looking for references to external content and then imports and inlines them directly into your HTML.

```text
arweave deploy my-hello-world-demo/index.html --package
```

If you want to see how you file will be packaged before deploying then you can use the package command to test a packaged version of your file.

```text
arweave package path-to-my-app/index.html my-packaged-output.html
```

### Examples

**Using the** `--package` **flag**

[http://arweave.net/cxsNxKLNEzbCFu7\_v7kYbp9Fpq0NWuDPcEieDsuYkHk](http://arweave.net/cxsNxKLNEzbCFu7_v7kYbp9Fpq0NWuDPcEieDsuYkHk)

[https://github.com/ArweaveTeam/arweave-deploy/blob/master/sample/packaged/output.html](https://github.com/ArweaveTeam/arweave-deploy/blob/master/sample/packaged/output.html)

**Without using the** `--package` **flag**

[https://arweave.net/Oovrc3nWTpx3fAige-PuHQVnA1ebpJoGPxo1kLxJ3P8](https://arweave.net/Oovrc3nWTpx3fAige-PuHQVnA1ebpJoGPxo1kLxJ3P8)

[https://github.com/ArweaveTeam/arweave-deploy/blob/master/sample/original/index.html](https://github.com/ArweaveTeam/arweave-deploy/blob/master/sample/original/index.html)

#### Style sheets

This style sheet reference

```markup
<link rel="stylesheet" href="assets/style.css">
```

Becomes this

```markup
<style>
body {
    background: #383B44;
    text-align: center;
}

.content{
    margin: 10% auto;
    font-family: Arial, Helvetica, sans-serif;
    font-size: 1.5rem;
    color: #FFFFFF;
}
</style>
```

#### JavaScript

This JavaScript reference

```markup
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.3.1/jquery.js"></script>
```

Becomes this

```markup
<script>!function(e,t){"use strict";"object"==typeof module&&"object"==typeof module.exports?module.exports=e.document?t(e,!0):function(e){if(!e.document)throw new Error("jQuery requires a window with a document");return t(e)}:t(e)}("undefined"!=typeof window?window:this,function(e,t){"use strict";var n=[],r=e.document...
```

#### Images

This image reference

```markup
<img src="https://ichef.bbci.co.uk/news/660/cpsprodpb/71E1/production/_99735192_gettyimages-459467912.jpg" alt="A permanent cat picture">
```

Becomes this

```markup
<img alt="A permanent cat picture" src="data:image/jpeg;base64,/9j/4AAQSkZJRgABAQEAYABgAAD/2wBDAAYEBQYFBAYGBQYHBwYIChAKCgkJChQODwwQFxQYGBcUFhYaHSUfGhsjHBYWICwgIyYnKSopGR8tMC0oMCUoKSj/2wBDAQcHBwoIChMKChMoGhYaKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCj...
```

