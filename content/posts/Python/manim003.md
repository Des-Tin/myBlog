---
title: "Manim003"
date: 2020-10-19T15:21:20+08:00
draft: false
categories: [ "Python" ]
Toc : true
tags: [ "Python", "Develop", ""]
share : true 
keywords: [ "Python" ]
---

{{< notice notice-tip >}}
项目组员：华昊辉、刘梓怡、王博源
指导老师：武湛
{{< /notice >}}

# **论<font style ="color:#FF7F50">Manim</font>在教学中的应用**  
## 项目介绍：  

​		长久以来教学的方式都在不断转换，向着更加简明直观、方便的方向发展。ppt，flash动画随之而来，但是他们并不是专门为教学设计的，使用起来多有不便，本项目就是针对教学过程中的一些内容使用专门性的数学解释工具来进行研究。下面是具体课题：  

- **课题：均值不等式链二元形式的几何证明**
## 工具介绍
![logo](/image/manim.png)  
  **<font style ="color:#FF7F50">Manim</font>** 是一个解释性数学视频的动画引擎。它由格兰特·桑德森（Grant Sanderson）编写，并通过其YouTube频道[3Blue1Brown广受欢迎](https://www.youtube.com/3blue1brown)。它用于以编程方式创建精确的动画，如3Blue1Brown 的视频所示。它是一个运行在**<font style ="color:#0DCADA">Python</font>**环境的动画引擎，通过简单的代码就可做到丰富多彩的动画，以及图像。  其**效果**如下图所示：
  <img src="/image/azdqn-46w69.jpg">

### 安装**<font style ="color:#FF7F50">Manim</font>**  
1. 安装**<font style ="color:#0DCADA">Python</font>**  

2. 安装**<font style ="color:#FF7F50">Manim</font>**的依赖文件  

3. 安装**<font style ="color:#FF7F50">Manim</font>**  

   [在线Manim使用](https://www.eulertour.com/)
   
   具体步骤：详见[3Blue1Brown数学动画引擎Manim的Windows安装方法](https://www.bilibili.com/read/cv2282855?from=articleDetail)  
   
### **<font style ="color:#FF7F50">Manim</font>**使用实例 
   使用教程:[Manim-Kindergarten中文文档](https://manim.ml/getting_started/index.html)  
   因为manim制作的视频是没有声音的，因此只能使用后期配音加视频或者是只保留图像由老师在课堂上直接讲解。  

#### 题目  
$数学暑假作业(2)  函数的应用  第17题$

$\text{已知函数}f(x)=x^2+mx-1\text{，对于任意}x\in[m, m+1]\text{都有}f(x) < 0\text{成立，求}\text{实数}m\text{的取值范围}$

解题：

$ \text{易得：}  \frac{\sqrt{2}}{2}<m<\frac{\sqrt{2}}{2} , \frac{3}{2}<m<0$

$求得: \frac{\sqrt{2}}{2}<m<0$

深化：对于该题，初次见到的学生需要理解为什么需要分别将$m$和$m+1$代入到函数当中。而课堂上使用常规方式画出的图像实际并不能使学生 **<font style ="color:#FF7F50">直观</font>**，**<font style ="color:#FF7F50">充分</font>**地理解问题，而**<font style ="color:#FF7F50">Manim</font>**的使用则可以方便教师来结合 “班班通”使得教学更加方便。

#### **<font style ="color:#FF7F50">Manim</font>**代码编写

代码部分的说明：
1. “<font style ="color:#FF7F50">"""</font>” 和“<font style ="color:#FF7F50">"""</font>”之间的文字是对下面数行代码的注释。  

2. 左侧的数字则代表行号。

3. 数学公式使用的是$LaTeX$公式
   源代码详见 附件q.py

```python
from manimlib.imports import *

class vedio(Scene):
    def construct(self):
        """
        视频封面
        """
        title = TextMobject("数学暑假作业(2)  函数的应用  第17题")
        title.scale(1.5)
        author = TextMobject("讲解：华昊辉")
        author.shift(DOWN)
        self.play(Write(title), Write(author))
        self.wait(2)
        self.clear()
        """
        题目，导入
        """
        que1 = TexMobject(r"\text{17.已知函数}",
                          r"f(x)=x^2+mx-1",
                          r"\text{，对于任意}",
                          r"x\in[m, m+1]")
        que2 = TexMobject(r"\text{都有}",
                          r"f(x) < 0",
                          r"\text{成立，求}",
                          r"\text{实数}",
                          r"m",
                          r"\text{的取值范围}")
        que1.shift(UP * 3 + LEFT * 0.65)
        que2.shift(UP * 3 + LEFT * 2.5 + DOWN)
        self.play(Write(que1), Write(que2))
        self.wait(13)
        self.play(ApplyMethod(que1[1].set_color, TEAL_C), ApplyMethod(que1[3].set_color, TEAL_C),
                  ApplyMethod(que2[1].set_color, TEAL_C),
                  ApplyMethod(que2[3].set_color, TEAL_C), ApplyMethod(que2[4].set_color, TEAL_C))
        self.wait(9)
        self.clear()
        """
        解析函数图像
        """
        mt = TextMobject('$m =$')
        mt.shift(UR * 3)
        m = DecimalNumber(-2).scale(2)
        dm = m.get_value()
        m.scale(0.45)
        m.next_to(mt)
        axes = Axes(
            number_line_config={"color": LIGHT_GREY,
                                "include_tip": True,
                                "exclude_zero_from_default_numbers": True,
                                },
            x_min=-10, x_max=6,
            y_min=-7, y_max=3.5,
            center_point=ORIGIN
        )
        axes.add_coordinates()
        self.add(axes.get_axis_labels())

        func = FunctionGraph(
            lambda x: x ** 2 + dm * x - 1,
        )

        funcf = FunctionGraph(
            lambda x: x ** 2 + 2 * x - 1,
        )

        l1 = Line(np.array([dm, 7, 0]), np.array([dm, -7, 0]))
        l2 = Line(np.array([dm + 1, 10, 0]), np.array([dm + 1, -10, 0]))

        l1f = Line(np.array([2, 7, 0]), np.array([2, -7, 0]))
        l2f = Line(np.array([2 + 1, 10, 0]), np.array([2 + 1, -10, 0]))

        l1.set_color(RED)
        l2.set_color(RED)
        l1f.set_color(RED)
        l2f.set_color(RED)
        m.set_color(BLUE)
        mt.set_color(BLUE)
        self.play(Write(axes),
                  Write(func),
                  Write(l1),
                  Write(l2),
                  Write(mt),
                  Write(m))
        self.wait(21)
        self.play(ChangeDecimalToValue(m, 2),
                  ReplacementTransform(l1, l1f),
                  ReplacementTransform(l2, l2f),
                  ReplacementTransform(func, funcf),
                  run_time=10, rate_func=linear)
        self.clear()

        """
        解题
        """
        self.add(que1, que2)
        self.wait(61)
        r1 = TexMobject(r"f(m)=m^2+m^2-1<0")
        r2 = TexMobject(r"f(m+1) = (m+1)^2 + m(m+1) - 1 < 0")
        r = TextMobject("综上，解得：$-\\frac{\\sqrt{2}}{2}<m<0$")
        r.shift(DOWN * 2)
        r2.shift(DOWN)
        self.play(Write(r1), Write(r2), run_time=6)
        self.wait(2)
        r1f = TextMobject("$-\\frac{\\sqrt{2}}{2}<m<\\frac{\\sqrt{2}}{2}$")
        r2f = TextMobject("$-\\frac{3}{2}<m<0$")
        r2f.shift(DOWN)
        self.play(ReplacementTransform(r1, r1f), ReplacementTransform(r2, r2f), Write(r))
        self.wait(5)
        self.clear()
```


## 课题-均值不等式链二元形式的几何证明

### 研究背景以及目的

<center><video width="512" height="288" controls>
  <source src="/video/Intro_inequality.mp4" type="video/mp4">
您的浏览器不支持 video 标签。
</video></center>

​		在高中数学必修5的第三章中，我们学习了不等式。学习到了一个重要的概念——“均值不等式链”，在函数极值和数列求和中广泛使用。但是我们对于均值不等式却没有进行统一的证明。

​		该课题的目的在于使用几何方法，对均值不等式链$\frac{2}{\frac{1}{a}+\frac{1}{b}}\le\sqrt{ab}\le\frac{a+b}{2}\le\sqrt{\frac{a^2+b^2}{2}}$进行证明。

### 研究过程

#### 1 对$\sqrt{ab}\ge\frac{a+b}{2}$的证明		

​		<img src="/image/%E8%AF%BE%E9%A2%982.png" alt="课题2" style="zoom: 50%;" />  
<center><video width="512" height="288" controls>
<source src="/video/AM_GM.mp4" type="video/mp4">
您的浏览器不支持 video 标签。
</video></center>


如图以$A$点为圆心作圆，动点$M$在圆周上，过$M$做$GM\bot$圆的直径。连接点$M$与点$A$直径的两端点，取$MG$分直径得的线段分别为$a$、$b$。

$I$：由射影定理可得：$GM=\sqrt{ab}$

$II$：$AM$为圆的半径，由圆的性质得$AM=\frac{a+b}{2}$

$III$：随着点$M$在圆周上运动，$a, b$的值也随之改变，由线线垂直的性质可得$MG\ge AM$，即$\sqrt{ab}\le\frac{a+b}{2}$。

#### 2 将图形改进，以便推广到均值不等式中。

<img src="/image/%E8%AF%BE%E9%A2%982-1.png" alt="课题2-1" style="zoom:50%;" />  

<center><video width="512" height="288" controls>
  <source src="/video/HM_GM_AM_RM.mp4" type="video/mp4">
您的浏览器不支持 video 标签。
</video></center>

如图，过点$G$作$GH$垂直于$AM$，垂足为$H$，以$AG$为半径$A$为圆心做圆（虚线），做虚线圆半径$AR\bot AM$。

$I$：由相似可得$HM=\frac{2ab}{a+b}=\frac{2}{\frac{1}{a}+\frac{1}{b}}$

$II$：由勾股定理可得$RM=\sqrt{\frac{a^2+b^2}{2}}$

$III$：根据M点运动的规律来看，显然$HM\le GM\le AM\le RM$，即$\frac{2}{\frac{1}{a}+\frac{1}{b}}\le\sqrt{ab}\le\frac{a+b}{2}\le\sqrt{\frac{a^2+b^2}{2}}$。

## 项目的研究意义以及反思

​		Manim的使用能够使学生更好地理解和记忆公式。同时它的专业性使得数学、化学、物理的问题可以直观明了地揭示量化，几何关系：因为Manim的使用逻辑是基于数学的。

​		在可视化中，manim表现的不足之处在于：

   1. manim毕竟不是专门为了可视化而编写的，除了基本的形体、坐标轴、曲线等对象，manim没有专门为了可视化而封装的类或对象（比如我们需要做一个饼状图或柱状图，在matplotlib中我们直接有现成的类和方法，而在manim中得自己从头去做），我们当然可以在manim的基础上作出上限更高更美观漂亮的可视化结果，但还有很多时候，我们仅仅需要在几分钟内就能利用现有的数据和代码生成可视化结果；

   2. manim虽然能作出高质量的动画，但这些动画并不能实现和用户交互；
   
   3. 对于大量的二维/三维数据，manim的渲染效率应该不会太高（这点没有具体测试或数据上的支持，仅为主观猜测）。

## 参考资料：
 {{< notice notice-note >}}
 [MainimKindergarden中文网站]\(https://manim.ml/index.html)
 [Ciger666的Github开源仓库]\(https://github.com/cigar666/my_manim_projects)
 {{< /notice >}}