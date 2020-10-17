# slate-remark

![check](https://github.com/inokawa/slate-remark/workflows/check/badge.svg)

[remark](https://github.com/remarkjs/remark) plugin to transform remark synthax tree ([mdast](https://github.com/syntax-tree/mdast)) to [slate](https://github.com/ianstormtaylor/slate) document tree, and also slate to remark.

This plugin supports slate 0.50+.
And also support ~0.47.9 currently, but I don't know in the future.

## Demo

https://inokawa.github.io/slate-remark/

## Install

```
npm install slate-remark
```

## Usage

### Transform remark to slate

#### 0.50+

```javascript
import unified from "unified";
import markdown from "remark-parse";
import { remarkToSlate } from "slate-remark";

const processor = unified().use(markdown).use(remarkToSlate);

const res = processor.processSync(text).result;
console.log(res);
```

#### ~0.47.9

```javascript
import { Value } from "slate";
import unified from "unified";
import markdown from "remark-parse";
import { remarkToSlateLegacy } from "slate-remark";

const processor = unified().use(markdown).use(remarkToSlateLegacy);

const res = Value.fromJSON(processor.processSync(text).result);
console.log(res);
```

### Transform slate to remark

#### 0.50+

```javascript
import unified from "unified";
import stringify from "remark-stringify";
import { slateToRemark } from "slate-remark";

const processor = unified().use(slateToRemark).use(stringify);

const value = ...; // value passed to slate editor

const tree = processor.runSync({
  type: "root",
  children: value,
});
const res = processor.stringify(tree);
console.log(res);
```

#### ~0.47.9

```javascript
import unified from "unified";
import stringify from "remark-stringify";
import { slateToRemarkLegacy } from "slate-remark";

const processor = unified().use(slateToRemarkLegacy).use(stringify);

const value = ...; // value passed to slate editor

const tree = processor.runSync({
  type: "root",
  children: value.toJSON().document.nodes,
});
const res = processor.stringify(tree);
console.log(res);
```