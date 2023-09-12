# CSS 布局 (CSS layout)

## display属性

两个常用的布局 `display:flex` 和 `display: grid`

### [Flex 布局](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

应用此布局需要注意：

- 子元素的float，clear和vertical- align属性将会失效
- 采用 Flex 布局的元素，称为 Flex 容器（flex container），简称"容器"。它的所有子元素自动成为容器成员，称为 Flex 项目（flex item），简称"项目"。

#### *以下的6个属性是设置在容器上的：*
```
.container{
    display:flex; 
    # webkit内核的浏览器要这样写 display:-webkit-flex
    
    flex-direction: row | row-reverse | column | column-reverse;
    # row（默认值）：主轴为水平方向，起点在左端。--->
    # row-reverse：主轴为水平方向，起点在右端。<---
    # column：主轴为垂直方向，起点在上沿。子组件从上往下排
    # column-reverse：主轴为垂直方向，起点在下沿 子组件从下往上排


    flex-wrap: nowrap | wrap | wrap-reverse;
    # 子组件是否换行， 不换行/换行/换行，但是第一行在下面

    flex-flow: <flex-direction> || <flex-wrap>; 
    # 是上面两项的简写形式，比如 flex-flow:row nowrap

    justify-content: flex-start | flex-end | center | space-between | space-around;
    # 是主轴上的对齐方式，分别是左对齐，右对齐，居中对齐，两端对齐，每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

    align-items: flex-start | flex-end | center | baseline | stretch;
    # 属性定义项目在交叉轴上如何对齐，也就是与当前主轴垂直的轴
    # 如果主轴是横轴，---》 那么分别是，flex-start：从上往下，交叉轴起点对齐。flex-end：从下往上，交叉轴终点对齐。 center：居中对齐。 baseline：项目的第一行文字的基线对齐。stretch：如果项目未设置高度或者设置为auto，那么将占满整个容器的高度。

    align-content: flex-start | flex-end | center | space-between | space-around | stretch;
    # align-content属性定义了多根轴线的对齐方式，即设置了wrap or wrap-reverse的时候。如果项目只有一根轴线，该属性不起作用。
    # flex-start：与交叉轴的起点对齐。
    # flex-end：与交叉轴的终点对齐。
    # center：与交叉轴的中点对齐。
    # space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
    # space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
    # stretch（默认值）：轴线占满整个交叉轴。


    # 你也可以使用gap属性，不止适用于flex布局，也适用于grid 和 multi-column 布局
    gap: 10px;
    gap: 10px 20px; /* row-gap column gap */
    row-gap: 10px;
    column-gap: 20px;
    gap: calc(5vh + 5px) calc(5vw + 5px); 
    # you can also use calc() now no support for it on Safari and iOS.
 }
 ```

#### *以下的6个属性是设置在项目上的：*

```
.item{
    order: <integer>;  /* default 0 */
    # 定义项目的排列顺序。数值越小，排列越靠前，默认为0。

    flex-grow: <number>; /* default 0 */
    # 定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。
    # 如果所有项目的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。

    flex-shrink: <number>; /* default 1 */
    # flex-shrink属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。
    # 如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。负值对该属性无效。

    flex-basis: <length> | auto; /* default auto */
    # 定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。它可以设为跟width或height属性一样的值（比如350px），则项目将占据固定空间。

    flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
    # 是以上三个属性的简写，默认值为0 1 auto。后两个属性可选
    # 该属性有两个快捷值：auto (1 1 auto) 和 none (0 0 auto)。

}
```

### [Grid布局](https://css-tricks.com/snippets/css/complete-guide-grid/)

应用此布局要注意：

- 设为网格布局以后，容器子元素（项目）的float、display: inline-block、display: table-cell、vertical-align和column-*等设置都将失效。
- 它将网页划分成一个个网格，有行(row)和（列），单元格（cell），网格线（grid line）
- Grid 布局的属性分成两类。一类定义在容器上面，称为容器属性；另一类定义在项目上面，称为项目属性。

```
.container{
    display:grid;
    #也可以设置成行内元素 inline-grid

    grid-template-columns: 100px 100px 100px; /*repeat(3,33.33%)*/
    # 定义每一列的列宽，可以是固定值，也可以是百分比，写几个就几列，也可以写repeat函数。

    grid-template-rows: 100px 100px 100px; /*repeat(3,33.33%)*/
    # 定义每一行的行高，可以是固定值，也可以是百分比，写几个就几行，也可以写repeat函数。

    # repeat()函数，第一个参数是重复的次数，第二个是重复的值。repeat(2, 100px 20px 80px);比如这个定义了六行/列，分别是100px，20px,80px,100px,20px,80px.

    # auto-fill/auto-fit关键字， repeat(auto-fill/auto-fit,100px),表示没列宽度100px,然后自动填充，直到容器不能放置更多的列， auto-fill/auto-fit的区别是，当容器足够宽，auto-fill会用空白填充剩余的，而auto-fit会尽量扩大每一个子项的宽度。

    grid-template-columns:100px 1fr 2fr
    # fr关键字 grid-template-columns: 1fr 1fr;如果两列的宽度分别是1fr和2fr，那么后面的是前面宽度的两倍，fr跟固定宽度搭配会非常方便

    grid-template-columns: 1fr 1fr minmax(100px, 1fr);
    # minmax()接受两个参数，最大值和最小值，就表示列宽不小于最小值不大于最大值。

    grid-template-columns: 100px auto 100px;
    # auto ，表示由浏览器自己决定长度

   
    grid-template-columns: [c1] 100px [c2] 100px [c3] auto [c4];
    grid-template-rows: [r1] 100px [r2] 100px [r3] auto [r4];
    # 网格线名称，可以设置网格线名称


    grid-row-gap: 20px;
    grid-column-gap: 20px;
    grid-gap: <grid-row-gap> <grid-column-gap>; /*简写，如果第二个值省略，默认两个值相同*/
    # grid-row-gap属性设置行与行的间隔（行间距），grid-column-gap属性设置列与列的间隔（列间距）。根据最新标准，上面三个属性名的grid-前缀已经删除，grid-column-gap和grid-row-gap写成column-gap和row-gap，grid-gap写成gap。

}
```


    

    



    





# CSS 架构
# 学会使用CSS modules