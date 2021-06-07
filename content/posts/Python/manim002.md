---
title: "论Manim在教学中的应用"
date: 2020-08-28T16:24:54+08:00
draft: false
categories: [ "Python" ]
Toc : true
tags: [ "Python", "Develop", ""]
share : true 
keywords: [ "Python" ]
---
# **<font style ="color:#FF7F50">Manim</font>**  
![logo](/image/manim.png)  
​				**<font style ="color:#FF7F50">Manim</font>** 是一个解释性数学视频的动画引擎。它由格兰特·桑德森（Grant Sanderson）编写，并通过其YouTube频道[3Blue1Brown广受欢迎](https://www.youtube.com/3blue1brown)。它用于以编程方式创建精确的动画，如3Blue1Brown 的视频所示。它是一个运行在**<font style ="color:#0DCADA">Python</font>**环境的动画引擎，通过简单的代码就可做到丰富多彩的动画，以及图像。  其**效果**如下图所示：
<img src="/image/azdqn-46w69.jpg">

  

## 安装**<font style ="color:#FF7F50">Manim</font>**  
1. 安装**<font style ="color:#0DCADA">Python</font>**  

2. 安装**<font style ="color:#FF7F50">Manim</font>**的依赖文件  

3. 安装**<font style ="color:#FF7F50">Manim</font>**  

   [在线Manim使用](https://www.eulertour.com/)
   
   具体步骤：详见[3Blue1Brown数学动画引擎Manim的Windows安装方法](https://www.bilibili.com/read/cv2282855?from=articleDetail)  
   
## **<font style ="color:#FF7F50">Manim</font>**使用实例 
   使用教程:[Manim-Kindergarten中文文档](https://manim.ml/getting_started/index.html)  
   因为manim制作的视频是没有声音的，因此只能使用后期配音加视频或者是只保留图像由老师在课堂上直接讲解。  

### 题目  
$数学暑假作业(2)  函数的应用  第17题$

$\text{已知函数}f(x)=x^2+mx-1\text{，对于任意}x\in[m, m+1]\text{都有}f(x) < 0\text{成立，求}\text{实数}m\text{的取值范围}$

解题：

$ \text{易得：}  \frac{\sqrt{2}}{2}<m<\frac{\sqrt{2}}{2} , \frac{3}{2}<m<0$

$求得: \frac{\sqrt{2}}{2}<m<0$

深化：对于该题，初次见到的学生需要理解为什么需要分别将$m$和$m+1$代入到函数当中。而课堂上使用常规方式画出的图像实际并不能使学生 **<font style ="color:#FF7F50">直观</font>**，**<font style ="color:#FF7F50">充分</font>**地理解问题，而**<font style ="color:#FF7F50">Manim</font>**的使用则可以方便教师来结合 “班班通”使得教学更加方便。

### **<font style ="color:#FF7F50">Manim</font>**代码编写

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



### 效果展示  

见附件 manim002.mp4
<center><video width="512" height="288" controls>
  <source src="/video/manim001.mp4" type="video/mp4">
您的浏览器不支持 video 标签。
</video></center>

[下载pdf文档](https://desultory.icu/download/论Manim的教学使用.pdf)