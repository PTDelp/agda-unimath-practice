
# Style conventions for files

1. File names are descriptive of the concept it introduces, or the main theorem it proves. The file names could be considered indexing terms, with the list of files functioning much like the index in the back of a book. Usually, file names consist of a noun or a noun phrase. File names should be natural, sufficiently precise, concise, and consistent with those of related files. 
2. File names are entirely in lowercase, with words separated by hyphens. Words in file names should not be abbreviated unless the abbreviated term is a widely accepted mathematical term, e.g., `poset`.
3. Files that are part of the formalisation should be in literate agda using markdown. They should have the file extension `.lagda.md`.
4. Every file should begin with a header in the following format
```md
# The title of the file
```
5. Immediately after the header, there should be a block of Agda code that loads the options, declares the present module, and performs all the imports. In particular, there should be no further imports later on in the file.
6. The rest of the files is divided into sections, subsections and possibly subsubsections. `##` headings are the main sections of the page. Usually at the beginning we have `## Idea` describing informally the idea of the things in that file. Then we hav `## Definitions` for definitions, and after that `## Properties` followed by `## See also` and `## References`. In rare cases we can include a section `## Examples` for examples or `## Theorem` if the main purpose of the file is to prove an important theorem. The reason `## Examples` is rarely used is that usually examples go in their own files, which can be listed under `## See also`.
`###` headings are for subsectioning the `## Definitions` and `## Properties` section. They are brief descriptions of the code block that follows. If the code block that follows is very long, we can even use `####` headings to subdivide the subsections. 
Note that `#` headings are only used for the title of the page.
7. The subsections should have a markdown header of level `###` and they should concisely describe the content of the block of code that follows.

Ideally, the first section of a file explains the idea, then proceeds to give the main definition that is the focus of the current file, then proceeds possibly with examples and by deriving basic properties of the defined concept. We suggest adopting the following template:

```md
# The title of this file

[ module declaration]
[ import statements]

## Idea

( Informal description of the idea)

## Definitions

### Definition 1

( Contributor of this definition (optional))

[ formalization of the definition and immediately related structure]

## Examples

### X is an example

( Contributor of this definition (optional)
  Informal explanation)

[ formalization that X is an example]

### Y is an example

( Contributor of this example (optional)
  Informal explanation)

[ formalization that Y is an example]

## Properties

### Concise descrition of property 1

( Contributor of this property (optional)
  Informal explanation)

[ formalization of property 1]

### Concise description of property 2

( Contributor of this property (optional)
  Informal explanation)

[ formalization of property 2]
```

At the end of the file you may also add a `See also` or `References` subsection where you reference related sources such as other modules or articles related to the contents of the file.

- If you want to reference another module in the library use the pattern
  ```[`foundation.univalence-axiom`](foundation.univalence-axiom.md)```.
  This will be displayed as [`foundation.univalence-axiom`](foundation.univalence-axiom.md).
- If you want to reference another page with custom text use the pattern ```[Agda-Unimath](https://unimath.github.io/agda-unimath/)```.
  This will be displayed as [Agda-Unimath](https://unimath.github.io/agda-unimath/).
- If you want to reference another page without custom text but with a clickable link use the pattern ```<https://unimath.github.io/agda-unimath/>```.
  This will be displayed as <https://unimath.github.io/agda-unimath/>.
