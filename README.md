# heat
传热学大作业代码
作者：朱政海

# 内容介绍
本项目基于传热学大作业，题目要求如下：
    随着动力系统电气化的发展，动力电池在船舶、海洋平台、汽车等领域的应用日益广泛。 但是，动力电池的的性质深受温度影响，放电效率随温度的变化而变化，从而影响到电驱动 力系统的性能。例如，目前锂电池的工作温度范围宽为-20℃-60℃。在低温环境下，电动船 舶或电动汽车的续航里程会明显的缩减，甚至损失过半，连为“冷冰冰”的电池充电也是件困 难的事。而高温情况下，若没有合适的散热方案，电池包内各处温度将出现较大差异，影响 电池单体的一致性，严重时会引发电池过充导致“热失控”，进而使导致着火、爆炸。总之， 温控较差的电池，冬天在极北之地“病怏怏”，夏天在赤道可能“随时爆炸”。
    电池温控系统的设计至关重要。本作业任务为某锂电池模组设计散热方案，即散热的传 热方式、空间尺寸、材料选择及其物性，用数值求解的方法求得不同设计方案下的温度场分 布，以验证提出方案的有效性。
    本设计中，以磷酸铁锂电池为对象，电池模组工作的环境温度为 30℃，每个电池单体 放电电流 3A，内阻 10mΩ，电池单体尺寸 25mm*25mm*65mm（长宽高）。
    电池温控设计的评价指标：
    （1） 温度范围在-20℃-60℃之内；
    （2） 各电池单体的温度具有一致性，即不同电池单体间的温差小；
    （3） 成本低；

受该项目启发，作者制作了一个传热框架模型。为了能够适用于更多种类的电池甚至别的传热情况模拟，代码尽量以抽象的形式体现与计算。

# 函数功能与使用介绍
整个电池框架battery类 在 battery.py 文件中给出
## 默认参数介绍
    x_number=8,     //横向排布电池个数
    y_number=4,     //纵向排布电池个数
    size=25,        //单个电池尺寸（mm）
    interval=10,    //电池与边界、电池与电池的间隔距离（mm）
    room_temp=0,    //室内温度（等于边界外的恒温，也等于电池组内除电池外物质的初始温度）
    batt_temp=20,   //电池初始温度

## 建议访问的类数据:
    data            //温度矩阵，为二维模型中每个离散点的温度值
    prop            //物质矩阵，以数字的形式代表物质，在算例中默认节  空气：1 ，电池：10 水：100 ，硅胶：1000
                    //可以自定义物质类型
    
## 建议使用的函数：
    打印信息函数：
    real_info()     //实际电池组信息
    model_info()    //计算模型所需信息
    info()          //全部信息
    绘图函数：
    draw_heatmap()  //根据data矩阵图制热图
    draw_propmap()  //根据prop矩阵绘制物质图
    模型：
    left(add1,add2)
    right(add1,add2)
    up(add1,add2)
    down(add1,add2)         
                    //这四个函数功能相近，以left()为例，它会返回两个二维数组
                    //第一个是每个散点左侧的温度组成的矩阵，第二个是每个散点左侧的物质代数组成的矩阵
                    //由于在二维数组的边界处，无法寻找左侧函数的值，故有add1和add2参数，
                    //add1参数可以自定义边界温度，默认为室温
                    //add2参数可以自定义边界物质，默认为空气（即值为1）
    set_prop(type)  //设置物质类型
                    //type0:初始化 全部置零
                    //type1:充满空气
                    //type2:横排水管
                    //type3:横排硅胶
    step()          //由上一秒每个散点四周的物质属性、温度决定该点下一秒的温度
    
    //空气1 电池10 水100 硅胶1000
    //情况可能为2 20 200 1、2000 11 101 1001 110 1010

# 自定义模型



