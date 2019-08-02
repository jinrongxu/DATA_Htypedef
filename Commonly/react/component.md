###react组件
    1. react组件的名称，首字母要大写
    2. 定义组件的意义
    3. jsx中循环创建时，用map,因为map具有返回值;
    (用key的原因:作为一个唯一的标识,通过dif算法能够准确的检测局部的差异,再通过key值准确的找到需要更新的元素,提高性能)
    4. 若类组件使用了constructor()方法,就得使用super()


###无状态组件(函数定义组件 )
    1.无状态组件没有this
    2.没有生命周期
    3.不能定义状态(state)
    4.只能返回一个根节点元素
    5.不能通过this.props来调用
    6.不能被new



###扩展知识
    1.vue组件的概念:(扩展,封装)
    扩展html元素;封装可重用的代码
    2.v-bind动态传参   :tite='title'    
            静态传参    title=title



###笔记
    //设置props的默认值的两种方法
    1. 类名.defaultProps={//写在抛出之前

    }
    2. static defaultProps={//写在类里面,和render()同级。
        title:'颜茹玉'
    }




    //组件内部定义一个内部状态
    1. constructor(){//组件内部定义一个内部状态
        super();
        this.state={
            aaaa:'666'
        }
    } 
    2. state={//不写constructor的情况下，定义一个内部状态
        aaa:'666'
    } 