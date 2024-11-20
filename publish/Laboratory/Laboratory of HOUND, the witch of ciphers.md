---
aliases: 
cssclasses:
  - red-truth
  - red-links
---


## Crime scene of the [[Chapel]]
- abc
- 1234
- __im[[por]]tant [[red link]]__. Not important [[normal link]].

> [!NOTE|c-plain bg-plain]+ # Crime scene of the [[Chapel]]
> - Contents
> - abc
> - __im[[por]]tant [[red link]]__. Not important [[normal link]].


`/>\s*\[\![^\n]*\n(?:>\s*.*\n)*/g`

```dataview
table
"!"+file.link
from #callout 
```

`="!"+[[Callout3]].file.link`

### Yo, this is definitely going somewhere
- [ ] Inlude if first line contains one of Mystery, Deduction, Hypothesis. Else ignore
- [ ] Group by type
	- [ ] Separate views?
- [ ] Improve views
	- [ ] grid if possible
	- [ ] maybe cards
- [ ] Add views to canvas


```dataviewjs
const pages = dv.pages('')

// This regex will find the contents of a specifically formatted callout
//const regex = />\s\[\!NOTE\]\s(.+?)((\n>\s.*?)*)\n/
const regex = />\s*\[\![^\n]*\n(?:>\s*[^\n]*\n)*/g


const rows = []
for (const page of pages) { 
	const file = app.vault.getAbstractFileByPath(page.file.path)
	// Read the file contents 
	const contents = await app.vault.read(file) 
	// Extract the summary via regex 
	for (const callout of contents.match(new RegExp(regex, 'sg')) || []) { 
		if(callout.split('\n')[0].contains("Deduction")){
			//rows.push([callout.split('\n')[0], callout, page.file.link]) 
		}
		rows.push([callout.split('\n')[0], callout, page.file.link]) 
	} 
}

dv.table(['Type', 'Callout', 'Note'], rows)
```




