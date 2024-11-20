---
cssclasses:
  - cards
---


cards
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
//dv.table(['Type', 'Callout', 'Note'], rows)
dv.table(['Callout'], rows)
```
