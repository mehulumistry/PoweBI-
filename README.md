# PoweBI-
Steps need to follow for PowerBI installation

1) Basic Intial Command

pbiviz new Name
npm install

// Before running make sure you have installed certificate otherwise it will not run https on your local host

pbiviz start

2) Installing d3 by using npm

npm install d3@4.9.1 --save

3) Including d3 to the pbiviz.json

{
  "visual": {...},
  "apiVersion": ...,
  "author": {...},
  "assets": {...},
  "externalJS": [
    "node_modules/d3/d3.min.js"
  ],
  "style": ...,
  "capabilities": ...,
  "dependencies": ...
}

4) Installing bootstrap by using npm

npm install bootstrap --save

5) Include the import statement to the visual.less

@import (less) "node_modules/bootstrap/dist/css/bootstrap.css"; 
// its showing ERROR: LESS  style/visual.less : (1,63) 'bootstrap.css' wasn't found. Tried - bootstrap.css,bootstrap.css


6) Install d3 typings 

npm install @types/d3@3.5 --save-dev
