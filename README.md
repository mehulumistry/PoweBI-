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
// it will show error but can compile easily. ERROR: LESS  style/visual.less : (1,63) 'bootstrap.css' wasn't found. Tried - bootstrap.css,bootstrap.css


6) Install d3 typings 

npm install @types/d3@3.5 --save-dev

#################################################

Updated installation steps for POWER-BI 

2. Create a new visual

pbiviz new testVisual
cd testVisual


3. Install typings https://github.com/typings/typings

npm i -g typings


4. Add d3 v3.5.5

npm i d3@3.5.5 --save

5. Add d3 typing

typings install d3=github:DefinitelyTyped/DefinitelyTyped/d3/d3.d.ts#6e2f2280ef16ef277049d0ce8583af167d586c59 --global --save

6. Add files to tsconfig.json

{
  "compilerOptions": {
    "allowJs": true,
    "emitDecoratorMetadata": true,
    "experimentalDecorators": true,
    "target": "ES5",
    "sourceMap": true,
    "out": "./.tmp/build/visual.js"
  },
  "files": [
    ".api/v1.6.0/PowerBI-visuals.d.ts",
    "node_modules/powerbi-visuals-utils-dataviewutils/lib/index.d.ts",
    "src/settings.ts",
    "typings/index.d.ts",
    "src/visual.ts"
  ]
}

7. Add d3 reference to pbiviz.json to externalJS array

{
  "visual": {
    "name": "",
    "displayName": "",
    "guid": "",
    "visualClassName": "Visual",
    "version": "1.0.0",
    "description": "",
    "supportUrl": "",
    "gitHubUrl": ""
  },
  "apiVersion": "1.6.0",
  "author": {
    "name": "",
    "email": ""
  },
  "assets": {
    "icon": "assets/icon.png"
  },
  "externalJS": [
    "node_modules/powerbi-visuals-utils-dataviewutils/lib/index.js",
    "node_modules/d3/d3.min.js"
  ],
  "style": "style/visual.less",
  "capabilities": "capabilities.json",
  "dependencies": "dependencies.json",
  "stringResources": []
}


8. Copy this code to src/visual.ts

module powerbi.extensibility.visual {
    export class Visual implements IVisual {
        private target: HTMLElement;
        private settings: VisualSettings;
        private svg: d3.Selection<SVGElement>;

        constructor(options: VisualConstructorOptions) {
            let svg = this.svg = d3.select(options.element)
                .append('svg').classed('liquidFillGauge', true);

            this.svg.append("circle")
                .attr("cx", 50)
                .attr("cy", 50)
                .attr("r", 50)
                .style("fill", 'green');
        }

        public update(options: VisualUpdateOptions) {
        }

        public destroy(): void {
        }

        private static parseSettings(dataView: DataView): VisualSettings {
            return VisualSettings.parse(dataView) as VisualSettings;
        }

        public enumerateObjectInstances(options: EnumerateVisualObjectInstancesOptions): VisualObjectInstance[] | VisualObjectInstanceEnumerationObject {
            return VisualSettings.enumerateObjectInstances(this.settings || VisualSettings.getDefault(), options);
        }
    }
}

9. Start pbiviz server

pbiviz start

and run it on 8080 port





