### 白话文

>null： 你有一个种树的想法，圈一块地，说你要在这里种树；

>undefined：你有一个种树的想法，圈一块地，说你要在这里种树；同时你还挖了一个坑准备种树（仅仅是挖坑，也还没有种树）；


### 共性

在javascript里，null和undefined都表示不存在的数据，并且undefined也是从null中继承而来的;

null和undefined都是表示没有的，不存在的值；他们两个在进行逻辑转换时候都是false；这两个值进行比较是true；

Null和undefined没有toString方法；所以null和undefined和人和数据比较都是false；

因为undefined派生自null，所以undefined和null做数据类型比较的时候的true；

### 区别

null表示空引用，它是object类型，undefined表示未定义，它是undefined类型；

null是object类型，但不是object的实例；用instanceof为false；

Number(null) // 0    Number(undefined) // NaN;

### 历史

但是，JavaScript的设计者Brendan Eich，觉得这样做还不够，有两个原因。首先，null像在Java里一样，被当成一个对象。但是，JavaScript的值分成原始类型和合成类型两大类，Brendan Eich觉得表示"无"的值最好不是对象。其次，JavaScript的最初版本没有包括错误处理机制，发生数据类型不匹配时，往往是自动转换类型或者默默地失败。Brendan Eich觉得，如果null自动转为0，很不容易发现错误。
因此，Brendan Eich又设计了一个undefined。他是这样区分的：null是一个表示"无"的对象，转为数值时为0；undefined是一个表示"无"的原始值，转为数值时为NaN。
