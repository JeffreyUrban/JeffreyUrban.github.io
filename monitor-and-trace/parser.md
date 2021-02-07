---
title: Parser
parent: Monitor & Trace
---

# Perl

I can create a text filter for certain defined formats, such as `"key":value,`.  

Output timestamp, topic and value to a file for each topic/key pair. Suppress these from output, so I can see what's left and write more filters to handle them.  

[https://stackoverflow.com/questions/11844679/extraction-and-printing-of-key-value-pair-from-a-text-file-using-perl](https://stackoverflow.com/questions/11844679/extraction-and-printing-of-key-value-pair-from-a-text-file-using-perl)  

[https://www.perlmonks.org/?node\_id=694325](https://www.perlmonks.org/?node_id=694325)  

[https://perlmaven.com/perl-split](https://perlmaven.com/perl-split)  

# Python 

'data munging'

## JSON  

[https://docs.python-guide.org/scenarios/json/](https://docs.python-guide.org/scenarios/json/)  

[https://realpython.com/python-json/](https://realpython.com/python-json/)  

[https://docs.python.org/2/library/json.html](https://docs.python.org/2/library/json.html)  

Best if I can feed in known good JSON segments  

## Lexer and Parser  

[https://tomassetti.me/guide-parsing-algorithms-terminology/](https://tomassetti.me/guide-parsing-algorithms-terminology/)  

[https://tomassetti.me/parsing-in-python/](https://tomassetti.me/parsing-in-python/)  

### Parser generators

Parser generators support regular languages and context-free grammar languages.  

Consider one that supports multiple languages, like ANTLR, Pyleri, Canopy.
- ANTLR can parse binary data  
- Canopy has inline function feature \(useful?\), but may be limited to specific types of languages \(PGE\)  

Popularity via Google search results  
- ANTLR: 892,000 results, Canopy: 140,000 results, Pyleri: 10,100 results  

Parser combiner is simpler, good when regular expression is not enough.

#### ANTLR  

[https://www.antlr.org/](https://www.antlr.org/)  

##### Tutorials  

[https://tomassetti.me/antlr-mega-tutorial/](https://tomassetti.me/antlr-mega-tutorial/)  

[https://willowtreeapps.com/ideas/an-introduction-to-language-lexing-and-parsing-with-antlr](https://willowtreeapps.com/ideas/an-introduction-to-language-lexing-and-parsing-with-antlr)  

##### For syslogs  

[https://github.com/palindromicity/simple-syslog-5424](https://github.com/palindromicity/simple-syslog-5424)  

[https://www.antlr3.org/pipermail/antlr-interest/2007-June/021406.html](https://www.antlr3.org/pipermail/antlr-interest/2007-June/021406.html)  

[https://stackoverflow.com/questions/12410496/parsing-a-log-file-with-antlr](https://stackoverflow.com/questions/12410496/parsing-a-log-file-with-antlr)  

Syslog protocol: [https://tools.ietf.org/html/rfc5424](https://tools.ietf.org/html/rfc5424)  
