# ITS project
## Project and group presentation 
Our project involves the creation of new RDF triples for "Il Cenacolo di Andrea del Sarto, Ultima Cena". The goal is to enrich the ArCo knowledge graph, by adding detailed information about this artwork. 

**Members**:

+ Maurizio Pomarico
+ Maria Eleonora Gimelli


## Methodology
Our approach is based on the following methodology:

+ **[ArCo Knowledge Graph](http://wit.istc.cnr.it/arco/?lang=en)** to identify and explore the theme. This step involved examining existing data and determining areas where additional information could enhance the knowledge graph.
+ **[The ArCO SPARQL endpoint](https://dati.cultura.gov.it/sparql)** to write specific queries to extract relevant information and ensure that our additions would be accurately integrated with the existing data.
+ **Large Language Models (LLMs)**, specifically **ChatGPT** and **Gemini**, to research the topic, draft SPARQL queries and retrieve information as a question-answering tool.
To communicate effectively with the LLMs, we applied four prompting techniques:
    - **Zero-Shot**: Directly asking the LLMs to generate content without providing examples;
    - **Zero-Shot-CoT (Chain-of-Thought)**: Encouraging the LLMs to generate a logical sequence of thoughts or steps, enhancing the reasoning process;
    - **Few-Shot-CoT**: Providing a few examples to guide the LLMs in generating new content that aligns with our requirements;
    - **Generated Knowledge Prompting**: Using knowledge generated by the LLMs in previous interactions to inform and improve subsequent prompts, creating a feedback loop that enhances the quality and relevance of the output.
+ **GitHub** to create and publish this website where we documented the key steps involved in our project. 



 


#### h4 Heading
##### h5 Heading
###### h6 Heading


## Horizontal rules

___


## Emphasis

**This is bold text**

__This is bold text__

*This is italic text*

_This is italic text_


# Blockquotes

> Blockquotes can also be nested...
>> ...by using additional greater-than signs right next to each other...
> > > ...or with spaces between arrows.


# Lists

Unordered

+ Create a list by starting a line with '+', '-', or '*'
+ Sub-lists are made by identiting 2 spaces:
  - Marker character change forces new list start:
    * Ac tristique libero volutpat at
    * Facilitis in pretium nisl aliquet
    * Nulla volutpat aliquam velit
+ Very easy!

Ordered

1. Lorem ipsum dolor sit amet
2. Consectetur adipiscing elit
3. Integer molestie lorem at massa


## Code

Inline `code` 

Intended code

    // Some comments
    line 1 of code
    line 2 of code
    line 3 of code

Block code "fences"

```
Sample text here...
```

Syntax highlighting 

``` js
var foo = function (bar) {
  return bar++;
};

console.log{foo5));
```


## Links
[link text](http://dev.nodeca.com)

[link with title](http://nodeca.github.io/pica/demo/ "title text!")

## Images

![Minion](https://octodex.github.com/images/minion.pgn)

## The End!


   

