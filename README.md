# ITS project
## Project and group presentation 
Our project involves the creation of new RDF triples for "*Il Cenacolo di Andrea del Sarto, Ultima Cena*". The goal is to enrich the ArCo knowledge graph, by adding detailed information about this artwork. 

![Cenacolo](https://upload.wikimedia.org/wikipedia/commons/thumb/8/83/Andrea_del_Sarto_-_The_Last_Supper_-_WGA00389.jpg/1200px-Andrea_del_Sarto_-_The_Last_Supper_-_WGA00389.jpg)

**Members**:

+ Maurizio Pomarico
+ Maria Eleonora Gimelli


## Methodology
Our approach is based on the following methodology:

+ **[ArCo Knowledge Graph](http://wit.istc.cnr.it/arco/?lang=en)** to identify and explore the theme. This step involved examining existing data and determining areas where additional information could enhance the knowledge graph.
+ **[The ArCO SPARQL endpoint](https://dati.cultura.gov.it/sparql)** to write specific queries to extract relevant information and ensure that our additions would be accurately integrated with the existing data.
+ **Large Language Models (LLMs)**, specifically **[ChatGPT](https://chatgpt.com/)** and **[Gemini](https://gemini.google.com/app?hl=it)**, to research the topic, draft SPARQL queries and retrieve information as a question-answering tool.
To communicate effectively with the LLMs, we applied four prompting techniques:
    - **_Zero-Shot_**: Directly asking the LLMs to generate content without providing examples;
    - **_Zero-Shot-CoT (Chain-of-Thought)_**: Encouraging the LLMs to generate a logical sequence of thoughts or steps, enhancing the reasoning process;
    - **_Few-Shot-CoT_**: Providing a few examples to guide the LLMs in generating new content that aligns with our requirements;
    - **_Generated Knowledge Prompting_**: Using knowledge generated by the LLMs in previous interactions to inform and improve subsequent prompts, creating a feedback loop that enhances the quality and relevance of the output.
+ **[GitHub](https://github.com/)** to create and publish this website where we documented the key steps involved in our project. 

## Project phases
### 1. Topic identification 
In the initial phase of our project, our primary objectives were to identify a suitable topic and verify the availability of related data within the ArCo Knowledge Graph.
We used the Zero-Shot technique asking ChatGPT to generate a list of lesser-known painters based in Florence. Our hypothesis was that ArCo might have fewer entries concerning works by "minor" artists compared to well-known figures.

<img width="577" alt="Screenshot 2024-06-26 120120" src="https://github.com/Maurizio-dot/Maurizio-dot.github.io/assets/173699843/e37bcd50-6f29-46ed-bd95-bc384db8eec6">
![Cattura 1](https://github.com/Maurizio-dot/Maurizio-dot.github.io/assets/173814358/808ef577-f686-46c3-ba5d-4fa9ca5b4424)

From this list we selected Andrea del Sarto. To verify the existence of properties associated with Andrea del Sarto within ArCo, we formulated the following ASK query:
```
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX arco: <https://w3id.org/arco/ontology/arco/>
ASK { 
?author a arco:HistoricOrArtisticProperty ;
rdfs:label ?label 
FILTER(REGEX(?label,  "Andrea del sarto", "i"))
}
```

The answer is [TRUE](https://dati.cultura.gov.it/sparql?default-graph-uri=&query=PREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0D%0APREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0APREFIX+arco%3A+%3Chttps%3A%2F%2Fw3id.org%2Farco%2Fontology%2Farco%2F%3E%0D%0AASK+%7B+%0D%0A%3Fauthor+a+arco%3AHistoricOrArtisticProperty+%3B%0D%0Ardfs%3Alabel+%3Flabel+%0D%0AFILTER%28REGEX%28%3Flabel%2C++%22Andrea+del+sarto%22%2C+%22i%22%29%29%0D%0A%7D%0D%0A%0D%0A&format=text%2Fhtml&timeout=0&signal_void=on).

Using SPARQL, we proceeded to count and sort properties associated with Andrea del Sarto by ordering them in descending order ("ORDER BY DESC"):

```
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX arco: <https://w3id.org/arco/ontology/arco/>
PREFIX a-cd: <https://w3id.org/arco/ontology/context-description/>
PREFIX agent: <https://w3id.org/arco/resource/Agent/>
SELECT DISTINCT ?label COUNT(DISTINCT ?culturalProperty) AS ?n
WHERE {
?culturalProperty a arco:HistoricOrArtisticProperty ;
a-cd:hasAuthor ?author .
?author rdfs:label ?label
FILTER(REGEX(?label, "Andrea del Sarto", "i"))
}
ORDER BY DESC(?n)
LIMIT 100
}
```

[Results](https://dati.cultura.gov.it/sparql?default-graph-uri=&query=PREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0A+PREFIX+arco%3A+%3Chttps%3A%2F%2Fw3id.org%2Farco%2Fontology%2Farco%2F%3E%0D%0A+PREFIX+a-cd%3A+%3Chttps%3A%2F%2Fw3id.org%2Farco%2Fontology%2Fcontext-description%2F%3E%0D%0A+PREFIX+agent%3A+%3Chttps%3A%2F%2Fw3id.org%2Farco%2Fresource%2FAgent%2F%3E%0D%0A+SELECT+DISTINCT+%3Flabel+COUNT%28DISTINCT+%3FculturalProperty%29+AS+%3Fn%0D%0A+WHERE+%7B%0D%0A+%3FculturalProperty+a+arco%3AHistoricOrArtisticProperty+%3B%0D%0A+a-cd%3AhasAuthor+%3Fauthor+.%0D%0A+%3Fauthor+rdfs%3Alabel+%3Flabel%0D%0A+FILTER%28REGEX%28%3Flabel%2C+%22Andrea+del+Sarto%22%2C+%22i%22%29%29%0D%0A%7D%0D%0A+ORDER+BY+DESC%28%3Fn%29%0D%0A+LIMIT+100%0D%0A&format=text%2Fhtml&timeout=0&signal_void=on).  

With the quantitative data in hand, we need the titles of the entities we want to enrich. Therefore, we asked ChatGPT to formulate a query to identify all paintings associated with Andrea del Sarto, using the FILTER(REGEX) to match the names, eliminating duplicates with SELECT DISTINCT, and including dates if available using OPTIONAL:



 


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


   

