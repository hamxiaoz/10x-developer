# NW.js (node-webkit)

### Node-webkit
Xml parser:
- xml2js, uses libxml, slow!
- easysax, pure js, faster
- node-expat, uses native module, faster (The node-webkit has limitations on using native module: cannot rename, has to compile with hack version of gyp)
