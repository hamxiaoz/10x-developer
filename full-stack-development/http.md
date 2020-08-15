# HTTP

## HTTP Header

How to force download?

```text
res.writeHead(200, {
  'Content-Type': 'application/pdf',
  'Content-Disposition': 'attachment; filename=out.pdf'
});
```

