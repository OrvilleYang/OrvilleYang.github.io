---
layout:     post
title:      "打印手写体的方法"
subtitle:   "How to print handwritten fonts"
date:       2022-01-20 10:21:00
author:     "Orville Yang"
header-style: text
catalog: true
tags:
    - 折腾
    - 打印
    - 字体
    - 手写字体
    - 笔记
---

主要参考自：[Markdown 语法高亮显示说明](https://www.jianshu.com/p/158d4a69b10d)。 

# 方法1

## 步骤1

去各种字体网站下载手写体，例如：李国夫手写体、贱萌体、陈静的字、逐浪大雪钢笔体、逐浪小雪钢笔体等。

## 步骤2

使用Word宏自动调整每个字的大小、字体、上下位置、行间距。  

首先需要在Word中，依次打开`文件`、`选项`、`信任中心`、`信任中心设置`、`宏设置`，然后选择`启用所有宏`，点击`确定`。  
依次打开`视图`、`宏`，随便起一个名字，比如“字体修改”，随后粘贴对应宏的代码。

```vb
Sub 字体修改()
'
' 字体修改 宏
'
    Dim R_Character As Range


    Dim FontSize(5)
    ' 字体大小在5个值之间进行波动，可以改写
    FontSize(1) = "21"
    FontSize(2) = "21.5"
    FontSize(3) = "22"
    FontSize(4) = "22.5"
    FontSize(5) = "23"



    Dim FontName(3)
    '字体名称在三种字体之间进行波动，可改写，但需要保证系统拥有下列字体
    FontName(1) = "陈静的字完整版"
    FontName(2) = "萌妹子体"
    FontName(3) = "李国夫手写体"

    Dim ParagraphSpace(5)
    '行间距 在一定以下值中均等分布，可改写
    ParagraphSpace(1) = "12"
    ParagraphSpace(2) = "13"
    ParagraphSpace(3) = "20"
    ParagraphSpace(4) = "7"
    ParagraphSpace(5) = "12"

    '不懂原理的话，不建议修改下列代码

    For Each R_Character In ActiveDocument.Characters

        VBA.Randomize

        R_Character.Font.Name = FontName(Int(VBA.Rnd * 3) + 1)

        R_Character.Font.Size = FontSize(Int(VBA.Rnd * 5) + 1)

        R_Character.Font.Position = Int(VBA.Rnd * 3) + 1

        R_Character.Font.Spacing = 0


    Next

    Application.ScreenUpdating = True



    For Each Cur_Paragraph In ActiveDocument.Paragraphs

        Cur_Paragraph.LineSpacing = ParagraphSpace(Int(VBA.Rnd * 5) + 1)


    Next
        Application.ScreenUpdating = True


End Sub
```

**建议采用A5的活页纸，便于打印。**

# 方法2

可以试试[这个Python库](https://github.com/Gsllchb/Handright)，可以实现对每个单个字整体的水平位置、竖直位置和字体大小以及每个笔画的水平位置、竖直位置和旋转角度做随机扰动。

### 安装

```Python
pip install handright
```

### 使用示例

```Python
# coding: utf-8
from PIL import Image, ImageFont

from handright import Template, handwrite

text = "我能吞下玻璃而不伤身体。"
template = Template(
    background=Image.new(mode="1", size=(1024, 2048), color=1),
    font=ImageFont.truetype("path/to/my/font.ttf", size=100),
)
images = handwrite(text, template)
for im in images:
    assert isinstance(im, Image.Image)
    im.show()
```

# 方法3

可以使用方正出品的**手迹造字**APP，实现数字化自己的手写字体，然后再下载使用。

# 方法4

可以使用在线转换的Web应用，比如[萝卜工坊](http://www.beautifulcarrot.com/)，以实现文字到手写风格pdf的转换。