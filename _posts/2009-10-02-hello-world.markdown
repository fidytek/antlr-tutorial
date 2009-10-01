---
layout: post
title: Przykłady „hello world”
---

# {{ page.title }}

{% highlight antlr-java %}
grammar Expr;  
prog:   stat+ ;  
stat:   expr NEWLINE  
    |   ID '=' expr NEWLINE  
    |   NEWLINE  
    ;  
expr:   multExpr (('+'|'-') multExpr)*  
    ;  
multExpr  
    :   atom ('*' atom)*  
    ;  
atom:   INT  
    |   ID  
    |   '(' expr ')'  
    ;  
ID  :   ('a'..'z'|'A'..'Z')+ ;  
INT :   '0'..'9'+ ;  
NEWLINE:'\r'? '\n' ;  
WS  :   (' '|'\t'|'\n'|'\r')+ {skip();} ;
{% endhighlight %}

Gramatykę z pliku *T.g* kompilujemy tak:

{% highlight bash %}
$ java org.antlr.Tool T.g  # => TLexer.java TParser.java T.tokens
{% endhighlight %}

Do testowania gramatyki użyjemy programu *Test.java* wywołującego regułę początkową
`r` tej gramatyki i czytającego tekst ze *stdin*:

{% highlight java %}
import org.antlr.runtime.*;
public class Test {
    public static void main(String[] args) throws Exception {
        // create a CharStream that reads from standard input
        ANTLRInputStream input = new ANTLRInputStream(System.in);
        // create a lexer that feeds off of input CharStream
        TLexer lexer = new TLexer(input);
        // create a buffer of tokens pulled from the lexer
        CommonTokenStream tokens = new CommonTokenStream(lexer);
        // create a parser that feeds off the tokens buffer
        TParser parser = new TParser(tokens);
        // begin parsing at rule r
        parser.r();
    }
}
{% endhighlight %}

Po tych przygotowaniach, kompilujemy program *Test.java*
(wygenerowane pliki *\*.class* zostaną umieszczone w katalogu
*classes*), przechodzimy do katalogu *classes* skąd
uruchamiamy skompilowany program:

{% highlight bash %}
$ mkdir -p classes
$ javac -d classes Test.java TLexer.java TParser.java
$ cd classes
$ java Test
call foo ;
... wciskamy ctrl+d ...
invoke foo
{% endhighlight %}


<!-- Linki -->
