![](https://i.imgur.com/Wc1MguG.jpg)

Ultra simple map-a-directory-to-something-else

# Usage

```
$ wget "https://raw.githubusercontent.com/coderofsalvation/d2x/master/d2x"
$ chmod 755 d2x
$ d2x init        # create example theme + src-folder
$ d2x src html --server
[x] copying theme/assets => html/assets
[x] rendering src => html......[x] done
[x] starting server at port 8000
Serving HTTP on 0.0.0.0 port 8000 ...
$ ls html/*       # profit!
```

> NOTE: before you run `d2x src` make sure a `theme` + `src`-folder exists. [Here](https://raw.githubusercontent.com/coderofsalvation/d2x/master/theme.zip) you can download an example.

## features

* simplicity / zero dependencies (just bash)
* directory structure is the navigation
* transparent urls: `src/foo.txt` will be accessible as `html/foo.txt` and `html/foo.txt.html`
* easily to be used on embedded systems or to publish github/gitlab pages (see `.gitlab-ci.yml`)
* template language is bash
* easy writable plugins (in any language)
* easy to host from a subdirectory (just run `echo 'https://foo.com/my/sub/folder' > theme/url` like in `.gitlab.yml`)

> it only uses: cat sed find xargs test which grep ls

## What is a theme?

In the theme-dir you just put your custom html + bashfunctions, to transform the input-files.<br>
Lets take a look at the example theme:

```
theme/assets                # here you can put stuff like stylesheet or images
theme/index.html            # master template
theme/title                 # textfile with inline shellscript 
theme/foobar                # shellscript
theme/plugins/myplugin      # allows you to hook into d2x functions

theme/plugins/filetype/txt   
theme/plugins/filetype/png  # process every desirable extension here 
theme/plugins/filetype/html
theme/plugins/filetype/....

theme/render                # a helper, to be able to do $( render another.html ) inside html 
theme/rendermenu            # index.html calls by containing $( rendermenu )
```

Could it be any easier and unsafer?
Absolutely, the `index.html` even supports environvariables:

```
<html>
	<head>
		<title>$(render title) $(foobar) $HOME</title>
	</head>
	<body>
		 $( rendermenu   )

		<div class="content">
		<!-- content --> 
		</div>

	</body>
</html>
```

And this theme will basically process a given directory-structure (`src` in the example):

```
src/10 collection A/bar.html
src/10 collection A/foo.html
src/10 collection A/textfile.txt
src/20 collection B/flop.html
src/20 collection B/shader.frag
src/index.html
```

In theory you could also use this to generate photoalbums, productlistings, source-code documentation etc!

## Why

Natural selection does [not always lead to greater complexity](https://www.newscientist.com/article/dn13617-evolution-myths-natural-selection-leads-to-ever-greater-complexity/).<br>
Not being stuck in a rut (of zillion dependencies) is bliss.

## Inspiration / similar simplicity tools

* [Expose](https://github.com/Jack000/Expose)
* [ssg](https://www.romanzolotarev.com/ssg.html)
