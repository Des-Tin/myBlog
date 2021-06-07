---
title: "Manim的初应用"
date: 2020-08-05T12:37:27+08:00
draft: false
categories: [ "Python" ]
Toc : true
tags: [ "Python", "Develop", "Manim"]
share : true 
keywords: [ "Python" ]
---
## 关于Manim  

![manim](/image/python/manim.png)  
[Manim](https://github.com/3b1b/manim) 是一个解释性数学视频的动画引擎。它用于以编程方式创建精确的动画，如[3Blue1Brown](https://www.3blue1brown.com/) 的视频所示。

这次的[^MANIM]初应用是源自老师布置的讲解作业的。  
因为是函数的题目，于是想着可以用manim来丰富讲解的内容。  
<br>  
因为manim制作的视频是没有声音的，因此只能使用后期配音加视频的方式制作。  

## 代码  
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
        """
        结束
        """
        ty = TextMobject("谢谢观看！")
        self.play(Write(ty), ApplyMethod(ty.scale, 1.5))
        self.wait(2)
```
<br>  

## 视频  

<center><video width="512" height="288" controls>
  <source src="/video/manim001.mp4" type="video/mp4">
您的浏览器不支持 video 标签。
</video></center>
[^MANIM]: 这里我使用的manim是3Blue1Brown版本而非社区版。  