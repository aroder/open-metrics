```dataviewjs
const pages = dv.pages()
const tags = pages.tags.distinct().sort()

const makeTagCountTable = (allTags, tagDisplayName, tagPrefix) => {
	const headers = [tagDisplayName, 'Number of Metrics']
	const rows = allTags
	  .filter(t => t.startsWith(`${tagPrefix}/`))
	  .map(t => [
		dv.parse(`#${t}`),
	    pages.where(p => p.tags?.includes(t)).length
	  ])
	dv.table(headers, rows)	
}
let headers = ["Business Functions", "Number of Metrics"]

makeTagCountTable(tags, 'Business Functions', 'Function')
makeTagCountTable(tags, 'Business Models', 'Model')
makeTagCountTable(tags, 'Industries', 'Industry')

```
