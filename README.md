## Related posts for Octopress

This feature already exists in jekyll, enabling this feature in
octopress is a trival task.

See <http://jcftang.github.com/> for an example of its use, click into some of the posts to see.

Firstly add this to your `_config.yml` file

    lsi: true

The create a file such as `source/_includes/custom/asides/related.html` with the following content

	<section>
		<h1>Related Posts</h1>
		<ul class="posts">
		{% for post in site.related_posts limit:5 %}
			<li class="related">
			<a href="{{ root_url }}{{ post.url }}">{{ post.title }}</a>
			</li>
		{% endfor %}
		</ul>
	</section>

It is possible to style the list, but in the above I have chosen to keep
the same style as the recent posts.

Finally, add the file to your default asides list in your `_config.yml` file

	default_asides: [custom/asides/related.html, ...]

## Probable issues with enabling LSI

There are some issues with enabling LSI in jekyll/octopress, the primary
issue will be performance. The default implementation will be slow if
you have lots of posts to classify. It would be recommended that rb-gsl
be installed to accelerate the classification process.

### Errors when installing the rb-gsl gem
```
Building native extensions.  This could take a while...
ERROR:  Error installing gsl:
    ERROR: Failed to build gem native extension.

...

```

The gsl gem requires gsl 1.14. Installing gsl using apt-get or brew will get you 1.15, which leads to another error when installing the rb-gsl gem.

#### Linux fix
```
$ curl -O http://mirror.aarnet.edu.au/pub/gnu/gsl/gsl-1.14.tar.gz
$ tar xfz gsl-1.14.tar.gz
$ cd gsl-1.14
$ ./configure
$ make clean
$ make								# can take a while, be patient
$ sudo make install
$ gem install gsl
```

#### OSX fix
See http://bretthard.in/2012/03/getting-related_posts-lsi-and-gsl-to-work-in-jekyll/#.UEZRSLQgeoM
