[[Obsidian Tips and Tricks]]

A handy dataview table that can be put in notes to show all its backlinks

```
```dataview
TABLE WITHOUT ID file.link AS "Backlinks"
FROM [[#]]
WHERE file.name != this.file.name
```
```
