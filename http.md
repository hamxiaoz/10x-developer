# HTTP


## HTTP Header

How to force download?  
```
res.writeHead(200, {
  'Content-Type': 'application/pdf',
  'Content-Disposition': 'attachment; filename=out.pdf'
});
```
