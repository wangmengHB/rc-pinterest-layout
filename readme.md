# rc-pinterest-grid（react component）
English | [简体中文](./README-zh_CN.md)   

This is a react component which provides a pinterest layout grid, and :
1. no need to provide height for each block.   
2. the height of each block can be changed by user (etc reszie) while the grid can be relayouted automatically.  
3. support automatically responsive.    
4. support self-defined responsive.  

![demo1](https://raw.githubusercontent.com/wangmengHB/rc-pinterest-grid/master/images/demo1.png)


## install
```
npm install --S rc-pinterest-grid
```

## Usage
```jsx
import PinterestGrid from 'rc-pinterest-grid';
```

```jsx
<PinterestGrid
  columns={4}               // how many columns in one row
  columnWidth={200}         // width of each block
  gutterWidth={10}          // horizontal gutter between each block
  gutterHeight={10}         // vertical gutter between each block
>
  <div key="A">A</div>
  <div key="B">B</div>
  <div key="C">C</div>
  {
    // ... more blocks here
  }
</PinterestGrid>
```

### PinterestGrid Props
| Prop Name     | Description     | Type     |  Required  | Default |
| :----- | :------- | :------- | :----- | :----- |
| columns | it specifies how may columns in one row | number | true  | 4     |
| columnWidth | it specifies the width of every block | number | true | 200 |
| gutterWidth | horizontal gutter between each block | number | false  | 10     |
| gutterHeight | vertical gutter between each block | number | false | 10  |
| responsive  | whether to be responsive responding with the screen width  | boolean  | false  | false    |
| breakPoints | self-defined break point list for responsive, it works only if responsive props exist | BreakPoint[]  &#124; undefined | false   |   无   |

Note：
1. when `responsive` is true, and `breakPoints` not provided, it will be responsive in the default way.   
2. when `responsive` is true, and `breakPoints` provided, it will follow the self-defined breakPoints to be responsive to screen width.  


### BreakPoint 
| Prop Name     | Description     | Type     |  Required  | Default |
| :------- | :------- | :------- | :----- | :----- |
| minScreenWidth | min screen width for this break point，it should be 0 for first break point | number | true  | 无     |
| maxScreenWidth | max screen width for this break point, it should be Infinity for last break point | number | true  | 无 |
| columnWidth  | under this break point，the width for every block  | number  | true  | 无    |
| columns | under this break point, how many columns should be placed in one row | number | true   |   无   |


## Use Case 1： simple usage
```jsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import PinterestGrid from 'rc-pinterest-grid';

const list = [1,2,3,4,5,6,7,8,9,10,11,12];

const Demo = () => (
  <PinterestGrid
    columns={4}             // 一共有多少列
    columnWidth={200}     // 列宽度
    gutterWidth={10}     // 块之间的水平间隙
    gutterHeight={10}   // 块之间的上下间隙
  >
    { // 此处放置需要渲染的块
      list.map((item, index) => (
        <div key={index} className={...} style={...}>
          ...
        </div>
      ))
    }
  </PinterestGrid>
)

ReactDOM.render(<Demo />, root);

```

## Use Case 2：automatic responsive
```jsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import PinterestGrid from 'rc-pinterest-grid';

const list = [1,2,3,4,5,6,7,8,9,10,11,12];

const Demo = () => (
  <PinterestGrid
    columns={4}             
    columnWidth={200}     
    gutterWidth={10}     
    gutterHeight={10}   
    responsive={true}    
  >
    { 
      list.map((item, index) => (
        <div key={index} className={...} style={...}>
          ...
        </div>
      ))
    }
  </PinterestGrid>
)

ReactDOM.render(<Demo />, root);
```
![demo2](https://raw.githubusercontent.com/wangmengHB/rc-pinterest-grid/master/images/demo2.png)
![demo3](https://raw.githubusercontent.com/wangmengHB/rc-pinterest-grid/master/images/demo3.png)


## Use Case 3: self-defined responsive
```jsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import PinterestGrid from 'rc-pinterest-grid';

const list = [1,2,3,4,5,6,7,8,9,10,11,12];

// self-defined break points
const breakPoints = [
  {
    minScreenWidth: 0,
    maxScreenWidth: 300,
    columns: 1,
    columnWidth: 200,
  },
  {
    minScreenWidth: 300,
    maxScreenWidth: 900,
    columns: 2,
    columnWidth: 300,
  },
  {
    minScreenWidth: 900,
    maxScreenWidth: Infinity,
    columns: 3,
    columnWidth: 600,
  },
]

const Demo = () => (
  <PinterestGrid
    columns={4}            
    columnWidth={200}      
    gutterWidth={10}       
    gutterHeight={10}      
    responsive={true}             
    breakPoints={breakPoints}     
  >
    { 
      list.map((item, index) => (
        <div key={index} className={...} style={...}>
          ...
        </div>
      ))
    }
  </PinterestGrid>
)

ReactDOM.render(<Demo />, root);
```


## License
MIT

