```dataview  
list updated AS 最后更新  
WHERE contains(file.folder, this.file.folder)  
WHERE file.name != "index"  
WHERE share = true  
```