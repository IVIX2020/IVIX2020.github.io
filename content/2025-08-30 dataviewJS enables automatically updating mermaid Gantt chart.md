---
type: inbox
tags:
  - obsidian
  - mermaid
related:
---
```dataviewjs  
const fullFolder = dv.current().file.folder;  // ex: "parent/sub"  
const folderParts = fullFolder.split("/");  
// タイトルは親フォルダ（最上位）  
const title = folderParts[0];  
// ページを親フォルダ以下のすべて対象にする  
const pages = dv.pages()  
  .where(p => p.file.folder && p.file.folder.startsWith(title) && p.start && p.end);  
// サブフォルダ名（セクション）は親フォルダから一つ下の階層まで（例：parent/sub の"sub"）  
function getSection(p) {  
  const parts = p.file.folder.split("/");  
  return parts.length > 1 ? parts[1] : parts[0];  
}  
function toMermaidGantt(pages, title) {  
  // Mermaid初期化パラメータでバー高さ、フォントをカスタム  
  let mermaid = `%%{init: {  
    "themeVariables": {  
      "fontSize": "10px",  
      "barHeight": 15,  
      "barGap": 6,  
      "sectionFontSize": "14px",  
      "topPadding": 20,  
      "leftPadding": 15,  
      "rightPadding": 10,  
      "gridLineStartPadding": 15  
    }  
  }}%%  
gantt  
  title ${title}  
  dateFormat YYYY-MM-DD  
  `;  
  
  // セクションごとにグループ化  
  const grouped = {};  
  for (const p of pages) {  
    const section = getSection(p);  
    if (!grouped[section]) grouped[section] = [];  
    grouped[section].push(p);  
  }  
  for (const section in grouped) {  
    mermaid += `  section ${section}\n`;  
    for (const p of grouped[section]) {  
      const start = p.start.toISODate ? p.start.toISODate() : p.start;  
      const end = p.end.toISODate ? p.end.toISODate() : p.end;  
      const days = Math.ceil((new Date(end) - new Date(start)) / (1000*60*60*24)) + 1;  
      mermaid += `    ${[p.file.name](http://p.file.name/)} : ${start}, ${days}d\n`;  
    }  
  }  
  return mermaid;  
}  
const ganttCode = toMermaidGantt(pages, title);  
dv.el("pre", `\`\`\`mermaid\n${ganttCode}\n\`\`\``, { cls: "markdown" });  
  
```

## prospect
- express story with Gantt chart which synchronized with directories.