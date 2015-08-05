# query-script
###Using a static html site to run custom javascript for you.

Run javascript in someone's browser by putting it in a URL.

It's basically XSS on purpose.

##Simple usage
Point a browser to `index.html` with the querystring set to your javascript.  Your javascript will be executed.

JQuery, Lodash, and RequireJs are loaded before your code is.

The following variables are made public to you, for URL brevity in some common use-cases:

| var | value          |
|-----|----------------|
| r   | require        |
| $   | jQuery         |
| b   | jQuery('body') |
| h   | jQuery('head') |
| _   | Lodash         |

##Examples

https://cdn.rawgit.com/fenwick67/query-script/master/index.html?b.html(%27Hello,%20world!%27)

https://cdn.rawgit.com/fenwick67/query-script/master/index.html?alert("hello!")

Note that TinyUrl actually takes any queryString passed to it and re-appends it to the redirect URL.  You can use this to keep your URLs shorter without even needing to make a tinyUrl each time.

http://tinyurl.com/prnmr9s?while(1)alert("hello!")

Not all browsers will handle the un-URI-encoded URLs gracefully, so it is probably best to escape them.

##Security Stuff
###*Don't put this on a domain with any sensitive information!*
People could use this to harvest your users' cookies, localstorage etc.  It's literally just `eval()`-ing the querystring.  That said, storing anything in localStorage or cookies or whatever is not going to be private because anybody can write code against this URL.
