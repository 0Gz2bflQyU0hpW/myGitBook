### flex布局

> 前景提要：position、display、float 在实操中存在的棘手问题：
>
> 1. 在父容器里垂直居中一个块元素
>
> 2. 动态设置子项等量宽度/高度，无论还有多少剩余空间
>
> 3. 多列布局中所有子项高度相同，而不管子项实际内容

##### Flex container（Flex 容器）的6个属性

* `flex-flow`: ***row nowrap***
  
  * `flex-direction`: ***row*** | row-reverse | column | column-reverse  
    
    决定主轴的方向（即项目的排列方向）
    
  * `flex-wrap`: ***nowrap*** | wrap | wrap-reverse 
  
    默认情况下项目排在一条轴线上，如果一条轴线排不下该属性决定如何换行
  
* `🌟justify-content`:  ***flex-start*** | flex-end | center | space-between | space-around 

  项目在主轴上的对齐方式

* `🌟align-items`: ***stretch***| flex-start | flex-end | center | baseline 

  项目在交叉轴上如何对齐

* `align-content`: ***stretch*** | flex-start | flex-end | center | space-between | space-around  

  属性定义了多根轴线（在交叉轴方向上）的对齐方式，如果项目只有一根轴线，该属性不起作用

##### Flex item（Flex 项目）的6个属性

* `order`: ***0*** <number>

  定义项目的排列顺序。数值越小，排列越靠前

* `flex`: ***0 1 auto*** | auto (1 1 auto) | none (0 0 auto)
  
  * `flex-grow`:  ***0*** 
  
    项目的放大比例，0代表不放大
  
  * `flex-shrink`: ***1*** 
  
    项目的缩小比例，0代表不缩小
  
  * `flex-basis`: ***auto***(项目本来的大小) | inherit ｜ 一个后跟 "%"、"px"、"em" 或任何其他长度单位的数字
  
* `align-self`: ***auto***(继承父元素的 align-items 属性)

  设置单个项目有与其他项目不一样的对齐方式，覆盖 align-items 属性

##### 注意

1. **content –> width –> flex-basis (limted by max|min-width)**
   也就是说，如果没有设置flex-basis属性，那么flex-basis的大小就是项目的width属性的大小；如果没有设置width属性，那么flex-basis的大小就是项目内容(content)的大小

##### 实操

需求场景： 数据工场->新建作业｜数据工场->新建质量项目，实现类似Antd <Row> <Col>单页多卡片的弹性伸缩及换行

存在问题：当每行的卡片数量保持一致时，flex有较好的表现，当页面压缩出现不同数量卡片的行时，会出现 *卡片长短不齐* 的问题。

解决方案1: flex + @media 查询，当出现长短不齐的情况时，强制修改为统一长度

