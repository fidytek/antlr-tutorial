---
layout: post
title: Jekyll-Blog HOWTO
---

<blockquote>
<img src="../../../../images/alan-perlis.gif" alt="[Alan Perlis]" />
<p>
  Dealing with failure is easy: Work hard to improve. Success is also
  easy to handle: You've solved the wrong problem. Work hard to improve.
</p>
<p class="author">— Alan Perlis</p>
</blockquote>

# {{ page.title }}

## Markdown

Posty wpisujemy używając notacji Markdown.
Notacja jest opisana przez autora Johna Grubera 
w witrynie [Daring Fireball](http://daringfireball.net/projects/markdown/syntax).

## Kolorowanie kodu

Kod wpisujemy tak:

<pre>
&#123;% highlight ruby %&#125;
def foo
  puts 'foo'
end
&#123;% endhighlight %&#125;
</pre>

A tak to wygląda po podkolorowaniu:

{% highlight ruby %}
def foo
  puts 'foo'
end
{% endhighlight %}

Kod jest kolorowany przez narzędzie
[pygmentize](http://pygments.org/docs/cmdline/).
Wykonanie polecenia:

    pygmentize -L lexers
    ...
    * antlr-java:
        ANTLR With Java Target (filenames *.G, *.g)
    * antlr-ruby, antlr-rb:
        ANTLR With Ruby Target (filenames *.G, *.g)
    * bash, sh:
        Bash (filenames *.sh, *.ebuild, *.eclass)
    ...

wypisuje listę obsługiwanych języków programowania.
