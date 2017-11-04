---
title: Dom vs SAX vs StAX
date: 2017-10-26 03:03:27
tags: dev
---

## DOM
Build tree-model for whole XML document

  * Pros:
    Trace XML document forward and backward.

  * Cons:
    Need more memory than other XML parser.

## SAX
Event-driven parser base on **push** manner.

  * Pros:
    Faster than DOM parser and need less memory.

  * Cons:
    Can't random access XML document. 

## StAX
Similar SAX use event-driven, but it base on **pull** manner.

  * Pros:
    Faster than DOM parser and need less memory.

  * Cons:
    Can't random access XML document. 

## Conclusion
I'm using StAX parser due to it more like iterator that iterate the XML document, no need write handler for push manner that SAX use.

### _ref_:
* [Java Dom Parser, tutorialspoint](https://www.tutorialspoint.com/java_xml/java_dom_parser.htm)
* [Java SAX Parser, tutorialspoint](https://www.tutorialspoint.com/java_xml/java_sax_parser.htm)
* [Java StAX Parser, tutorialpoint](https://www.tutorialspoint.com/java_xml/java_stax_parser.htm)
* [Java SAX vs. StAX, Jenkov.com](http://tutorials.jenkov.com/java-xml/sax-vs-stax.html)
