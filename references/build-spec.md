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
├── ContentCard (60,470,960×870,白色悬浮卡片)  ← z 在 Hero 之上;高度固定,不随文字长短变化
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
| SchoolText | ⚠️ 翻译规则 | 英文校名**必须整段译成中文**,包括跟在后面的州/省/城市名。`Queen's University, Ontario` → `女王大学(安大略)`,**不能只写「女王大学」或写成「女王大学 Ontario」**;`University of California, Berkeley` → `加州大学伯克利分校`。 |

【可替换·紫色学校文字色】`#5035A8`
【可替换·蓝色学校文字色】`#14406E`

---

## 三、悬浮正文卡片 ContentCard

| 属性 | 值 |
|---|---|
| 位置/尺寸 | x=**60**, y=**470**, 960 × **870** |
| **高度必须写死,禁止 hug_contents** | ⚠️ 卡片高度**固定 = 870**(规格满高,底边 y=1340,与 slogan y=1382 间距 42)。文字少的海报也必须是满高,下半部分自然留白。**同一批次内必须用同一个值**:返修既有批次时,先读该批其它海报用的固定值并沿用(9-7补 = 877,9-11 = 870;两者差 7px,肉眼不可见)。 |
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

- **实测结论:SchoolChip 直接作为 Hero 的第 3 个子节点建即可,不需要 Move。**
  Hero 是 vertical auto-layout:RegionRow(y 84~132)+ PosterTitle(y 158~298)+ SchoolChip(y 324~423),**胶囊底边 423 < 卡片顶边 470**,所以卡片(虽然 z 在 Hero 之上)永远盖不到胶囊。省掉 `M` + `U(x:72,y:324)` 那套,也就彻底避开了"Move 后 y 残留 166、胶囊叠到标题上"的老 bug(该 bug 见本文件历史版本)。
- 只有在**胶囊底边会越过 470** 的异常情况下(例如改了 Hero 内边距/间距),才需要把 SchoolChip 移到海报 Frame 顶层、index 排在 ContentCard 之后,并在 `M` 之后立刻 `U` 重设 `x=72, y=324`。
- 建完后务必导出检查一次:胶囊被卡片切掉 = z 顺序问题;胶囊叠在标题附近 = y 残留;两者都要修。

---

## 六之二、学校胶囊宽度上限(会长到溢出)

- Hero 内可用宽度 = 1080 − 72×2 = **936**;胶囊宽 = 108(内边距 72 + 圆点 22 + 间距 14)+ 文字宽。
- **判据:胶囊右边界必须 ≤ 1008**(左 72 + 936)。超过 1008 就已经压出 Hero 的右边距;超过 1080 会被 Hero 直接裁掉,**文字缺一半**。
- 实测危险案例(52px 字号下):
  - `加州大学圣塔芭芭拉分校｜USNEWS100`(12 汉字 + 8 拉丁)≈ 1111 宽 → 被裁,右边界 1079+ → **必须降到 42px**(降到 945)
  - `明尼苏达大学双城分校｜USNEWS76`(10 汉字)≈ 1080 宽,右边界 1046 → **降到 48px**(降到 979)
- 安全参考:10 汉字以内的校名(如 `加州大学圣地亚哥分校｜USNEWS21` ≈ 872 宽)用 52px 没问题。
- 处理顺序:① 优先保留 52px;② 右边界 > 1008 就把该张的 SchoolText 降到 48 → 46 → 42(按实际测量调),**只改这一张**,不要动其他张。
- 校验:导出后在 y=330~415 区间逐行从右往左找第一个白色像素,取最大 x,应 ≤ 1008。

---

## 七、导出与交付

1. `export_nodes` 导出 PNG,`scale=1` → 得到 1080×1440。
2. 文件名 = 源图文件名,**一字不差**(含中文/空格/扩展名)。
3. 源图是 `.jpg` → 导出 PNG 后需转成**真 JPEG**(PIL 转换,quality=95),禁止 PNG 字节存 .jpg。
4. 存入 `输入文件夹/YYYY-MM-DD/`。
5. 像素校验:同内容参照差异 <5%,不同内容参照 >8%。
6. **源图一律保留在原文件夹,不删除、不移动**;海报单独存输出文件夹。

### 七之一、自动化校验脚本(每批必跑)

```python
# 1) 卡片底边 / 自然高度:从 y=1439 向上找最后一个三点全 ≥253 的行
cb = None
for y in range(1439, 500, -1):
    if all(px[x, y][k] >= 253 for x in (300, 540, 800) for k in range(3)):
        cb = y; break
# cb 就是卡片底边。设固定高度前:自然高 = cb-470,> 870 表示放不下,= 1439 表示已溢出画布
# 设固定高度后:cb 应统一 ≈ 1338~1340

# 2) 胶囊右边界:y=330~415 每行从右往左找第一个白色像素,取最大 x
mx = max(x for y in range(330, 416) for x in range(1079, 0, -1)
         if px[x, y][0] > 245 and px[x, y][1] > 245 and px[x, y][2] > 245)
# mx 必须 ≤ 1008

# 3) 结构检查:每张海报 Frame 的直接子节点应为 Hero + ContentCard + WM×4 + Slogan = 7 个
#    少水印 / 页面顶层多出 WM 节点 → 用 M(WM节点id, 海报frame的id) 移回去
```

保存图片时:Ardot 导出的 PNG 可能是 **P 模式(调色板)+ 透明**,必须先 `convert("RGB")`(带 alpha 的先贴白底);源图是 `.jpg` 的用 **JPEG(quality=95, subsampling=0)** 保存,禁止把 PNG 字节存成 `.jpg`。

### 七之二、Offer(蓝色)模板

- `博士OFFER来啦!` + 蓝色渐变(见第一、二节蓝色值)。
- Offer 信/录取 PDF 常常**没有称呼语** → 省略 `DearRow`,正文从 `Line2` 开始。
- 红框(HighlightBox)放硬信息:录取项目 / 开学日期 / 学制 / 学费;`Line4` 用信里的落款语 + 签名马赛克。
- 输入是 PDF 时:输出名 = 原 PDF 名换成 `.png`,原 PDF 保留不动。
