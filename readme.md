# Org Anki Exporter

To use put the following into your .emacs

 (require 'ox-anki)

and then export with `C-c C-e a b` or `C-c C-e a f` from an org buffer.

The exported format is tab separated text file which is ready for Anki
import. The text file contains 4 columns: ID, Question, Answer, TAGS

## Writing questions in Org form

Headlines up to `org-export-headline-levels` (3 by default) are considered part
of the question. Everything contained in the last headline is considered to be
an answer.

So, for example

```org
* Good Guy?
  The Biscuit
* Bad Guy
** Where?
   Far Far Away
** When?
   Long Long Ago
** Who?
   Prince Charming
```
is converted into something along the following lines:

```html
fb28ecd4-5ee7-4b93-b3c6-631c2b19fd6f	Good Guy?	<div class="outline-text-2" id="text-1"><br><p><br>The Biscuit<br></p><br></div><br>

34c29a75-2bf6-4031-a254-6f265155ddb6	Bad Guy?<br>Where?	<div class="outline-text-3" id="text-2-1"><br><p><br>Far Far Away<br></p><br></div><br>
f1b512de-0b1b-4475-b701-2ad27dde09c4	Bad Guy?<br>When?	<div class="outline-text-3" id="text-2-2"><br><p><br>Long Long Ago<br></p><br></div><br>
826f883c-777e-4bb8-89d5-b6b81140c463	Bad Guy?<br>Who?	<div class="outline-text-3" id="text-2-3"><br><p><br>Prince Charming<br></p><br></div><br>
```

Though simple, this structuring of questions is very convenient because it
allows hierarchical construction of the questionnaires by topic. By using
org-mode visibility cycling (`Shift-TAB`) you can preview all the questions
without seeing the answers:

```org
* Good Guy?...
* Bad Guy
** Where?...
** When?...
** Who?..
```


## TODO
- Implement TAGS
- Export into `ID, H1, H2, H3, Answer, TAGS` format.
- Export selected properties as fields (also allow blanks with answers stored in
  properties). This would allow uniform treatment of ID property as well.
- Adjust latex export
- Images
- maybe: Figure out how ox manipulates the document tree and make the
  replication directly on the tree rather than with string splitting of the
  contents.