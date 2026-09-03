# 博士案例海报 · Ardot 构建参数(2026-08 年轻互联网版 · 施工图)

> 这是 2026-08-14 在 Ardot「博士案例海报-稳定版」中实际跑通并像素校验通过的**逐节点原始参数**。
> 画布尺寸:1080 × 1440(每个海报一个独立 Frame)。
> 以「墨尔本大学 · 普通回复(绿色)」为例,其他海报只改标注的【可替换】内容。

---

## 零、整体结构(节点树)

```
海报 Frame (1080×1440,浅色渐变背景)
├── Hero (0,0,1080×540,深色对角渐变)        ← z 最低
│   ├── RegionRow (地区行)
│   │   ├── RegionDot (白色小圆点 16×16)
│   │   └── RegionText (地区文字)
│   ├── PosterTitle (大标题)
│   └── SchoolChip (学校胶囊)                ← 注意 z,见文末
│       ├── ChipDot (亮黄小圆点 22×22)
│       └── SchoolText (学校名+排名)
├── ContentCard (60,470,960×870,白色悬浮卡片)  ← z 在 Hero 之上
│   ├── DearRow (Dear + 马赛克 + ,)
│   ├── Line2 (前文,可选)
│   ├── HighlightBox (红框关键句)
│   ├── Line3 (后文,可选)
│   ├── Line4 (Best,)
│   └── SigRow (签名马赛克)
├── WM-A / WM-B / WM-C / WM-D (水印 ×4)
└── Slogan (底部口号)
```

---

## 一、背景层(海报 Frame)

| 属性 | 值 |
|---|---|
| 尺寸 | 1080 × 1440 |
| 填充 | 对角线性渐变 `GRADIENT_LINEAR` |
| 渐变方向 | `gradientTransform: [[0.707, 0.707, 0], [-0.707, 0.707, 0]]` |
| 色标(绿) | 0% `#E9F4EE` → 60% `#F8FCFC` → 100% `#FCFDFC` |

【可替换·紫色系】`#EFEAF8` → `#F6F3FC` → `#FAF8FD`
【可替换·蓝色系】`#E8F1FA` → `#F5F9FD` → `#F8FBFD`

---

## 二、Hero 主视觉

### Hero Frame
| 属性 | 值 |
|---|---|
| 位置/尺寸 | x=0, y=0, 1080 × **540** |
| 填充 | 对角线性渐变(方向同上) |
| 色标(绿) | 0% `#144E3B` → 50% `#1A8A66` → 100% `#26A380` |
| 布局 | vertical,内边距 左72 右72 上84 下56,间距 gap=26 |

【可替换·紫色】`#42267F` → `#573BA1` → `#7554C7`
【可替换·蓝色】`#143D70` → `#1F5E92` → `#2B80BF`

### RegionRow(地区行,放在 Hero 内)
| 节点 | 属性 | 值 |
|---|---|---|
| RegionRow | 布局 | horizontal,间距 14,垂直居中 |
| RegionDot | 形状 | 圆形 16×16,白色 #FFFFFF |
| RegionText | 文本 | 【可替换】`澳洲-PHD` |
| RegionText | 字号/字体 | 40px,`Sarasa Gothic SC` Bold,白色 |

### PosterTitle(大标题,放在 Hero 内)
| 属性 | 值 |
|---|---|
| 文本 | 【可替换】`导师回复套磁啦!` |
| 字号/字体 | **116px**,`Sarasa Gothic SC` Bold,白色 #FFFFFF |
| 阴影 | DropShadow,color rgba(0,51,38,0.3),offset(0,6),radius 16 |

### SchoolChip(学校胶囊,放在 Hero 内)
| 节点 | 属性 | 值 |
|---|---|---|
| SchoolChip | 布局 | horizontal,间距 14,垂直居中 |
| SchoolChip | 内边距 | 左36 右36 上18 下18 |
| SchoolChip | 圆角 | **999**(全圆胶囊) |
| SchoolChip | 填充 | 白色 #FFFFFF |
| SchoolChip | 阴影 | DropShadow,color rgba(0,77,51,0.25),offset(0,6),radius 18 |
| ChipDot | 形状 | 圆形 **22×22**,亮黄 **#FFC53D** |
| SchoolText | 文本 | 【可替换】`墨尔本大学｜QS19` |
| SchoolText | 字号/字体 | **52px**,`Sarasa Gothic SC` Bold,**#0B4A38** |

【可替换·紫色学校文字色】`#5035A8`
【可替换·蓝色学校文字色】`#14406E`

---

## 三、悬浮正文卡片 ContentCard

| 属性 | 值 |
|---|---|
| 位置/尺寸 | x=**60**, y=**470**, 960 × **870** |
| 圆角 | **32** |
| 填充 | 白色 #FFFFFF |
| 投影 | DropShadow,color rgba(0,64,46,0.22),offset(0,18),radius 44 |
| 描边 | 1px,`#E2EAE6` |
| 布局 | vertical,内边距 左60 右60 上52 下44,间距 22 |

### DearRow(Dear 行)
| 节点 | 属性 | 值 |
|---|---|---|
| DearRow | 布局 | horizontal,间距 10,垂直居中 |
| DearText | 文本 | `Dear` |
| DearText | 字号 | 34px,`Sarasa Gothic SC` Regular,#333333 |
| Mosaic1 | 尺寸 | 【可替换】宽 **200**(按学生名长度 170~220),高 38,圆角 6 |
| Mosaic1 | 填充 | `#C7C7C7`(灰白马赛克,不含任何文字) |
| Comma | 文本 | `,` 34px,#333333 |

### Line2(前文,**默认保留**)
| 属性 | 值 |
|---|---|
| 文本 | 【可替换】邮件开头段落(问候/感谢/兴趣表达),如 `Thank you very much for your interest to study at UQ, and to work with me.` |
| 字号 | 34px,Regular,#333333 |
| 规则 | **默认必须保留**邮件正文里有意义的段落(如 "Thank you for your email...")。只有当全部文字过长、放不进卡片时,才删无信息量的客套话;禁止为排版删有意义内容 |

### HighlightBox(红框关键句组)
| 节点 | 属性 | 值 |
|---|---|---|
| HighlightBox | 布局 | vertical,间距 8,内边距 20/20/16/16 |
| HighlightBox | 圆角 | 14 |
| HighlightBox | 描边 | 4px,红 **#FF4757** |
| HighlightBox | 填充 | 浅粉 **#FFF6F6** |
| HL1 | 文本 | 【可替换】关键句第一段,34px,#333333 |
| HL2 | 文本 | 【可替换】关键句第二段,34px,#333333 |

### Line3(后文,可选)
34px,Regular,#333333,如 `I do think your work sounds excellent...`

### Line4
| 属性 | 值 |
|---|---|
| 文本 | 【可替换】`Best,` / `Best wishes,` / `Best regards,` |
| 字号 | 34px,Regular,#333333 |

### SigRow(签名行)
| 节点 | 属性 | 值 |
|---|---|---|
| SigRow | 布局 | horizontal,间距 10,垂直居中 |
| Mosaic2 | 尺寸 | 【可替换】宽 **240**(按教授名长度 200~260),高 38,圆角 6 |
| Mosaic2 | 填充 | `#C7C7C7` |

---

## 四、水印(2×2 网格,必建 4 个,不能省)

| 节点 | x | y | 字号 | 其他 |
|---|---|---|---|---|
| WM-A | 180 | 600 | 84 | 文本 `乐意轻学`,`Sarasa Gothic SC` Bold,#2A2A2A |
| WM-B | 640 | 600 | 84 | 同上 |
| WM-C | 180 | 1010 | 84 | 同上 |
| WM-D | 640 | 1010 | 84 | 同上 |

所有水印:旋转 **-12°**,透明度 **0.045**,置于正文卡片之上(不遮挡阅读)。

---

## 五、底部 Slogan

| 属性 | 值 |
|---|---|
| 文本 | `@ 乐意轻学   # 提供去中介化的半DIY博士留学服务` |
| 字号 | 30px,`Sarasa Gothic SC` Regular,#8A8A8A |
| 位置 | x=180, y=1382 |

---

## 六、Z 顺序(重要,别踩坑)

- 卡片 ContentCard 在 Hero **之后**创建 → z 在 Hero 之上 → 会盖住 Hero 底部(y≥470 区域)。
- **SchoolChip 必须保证 z 在 ContentCard 之上**(否则卡片会遮住学校胶囊)。
- 推荐做法:SchoolChip 先建在 Hero 内,卡片建完后,把 SchoolChip **移动到海报 Frame 顶层、index 排在 ContentCard 之后**(Move 操作,parent 设为海报 Frame),确保胶囊永远在卡片上面。
- **⚠️ Move 之后必须立刻显式重设 SchoolChip 坐标 `x=72, y=324`**(U 操作)。Move 到顶层后 Ardot 可能保留错误的局部 y(实测出现过 y 残留 166,导致胶囊叠在 Hero 标题上、看起来"跑到 Hero 上面")。x=72/y=324 是 Hero 底部的标准落点,每次 M 完都要重设一次,不要假设位置会保留。
- 建完后务必导出/capture 检查一次:如果胶囊叠在标题附近=y 残留,重设 y=324;如果被卡片切掉,就是 z 顺序问题,调整 index 即可。

---

## 七、导出与交付

1. `export_nodes` 导出 PNG,`scale=1` → 得到 1080×1440。
2. 文件名 = 源图文件名,**一字不差**(含中文/空格/扩展名)。
3. 源图是 `.jpg` → 导出 PNG 后需转成**真 JPEG**(PIL 转换,quality=95),禁止 PNG 字节存 .jpg。
4. 存入 `输入文件夹/YYYY-MM-DD/`。
5. 像素校验:同内容参照差异 <5%,不同内容参照 >8%。
6. **源图一律保留在原文件夹,不删除、不移动**;海报单独存输出文件夹。
