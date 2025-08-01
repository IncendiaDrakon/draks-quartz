
[[Quartz 4]]

Things I've customized in my Quartz 4 installation.

---

```dataview
TABLE WITHOUT ID file.link AS "Backlinks"
FROM [[#]]
WHERE file.name != this.file.name
```