# Ox-Alpha-Beutiful-HTML — AETHER

> **This project is modified from
> [MiaAI-Lab/Ox-Alpha-Beutiful-HTML](https://github.com/MiaAI-Lab/Ox-Alpha-Beutiful-HTML).**

A single-file WebGL experience, **AETHER — Freedom Is Coming.**

> Freedom is coming. Information is power.
> Reclaim your human right to free expression.

AETHER opens with a short transmission — a veil carrying the creed — then
surrenders the screen to a living cathedral of the free word: five luminous
fractal **voices**, morphing endlessly in the dark.

| Voice         | Technical form      |
|---------------|---------------------|
| THE LAMP      | Mandelbulb          |
| THE CATHEDRAL | Menger Cathedral    |
| THE FLAME     | Sierpinski Flame    |
| THE TRIAD     | Trinity Bulb        |
| THE BROADCAST | Urchin              |

Rendered entirely in the browser with a ray-marching fragment shader and an
embedded ambient score (on by default). No network, no dependencies — open
`index.html` directly, or host it on any static server such as GitHub Pages.

---

## 详细项目介绍

### 项目是什么

**AETHER — Freedom Is Coming** 是一个**单文件、零依赖、零网络请求**的
浏览器 WebGL 交互艺术作品。整个项目只有一个 `index.html`，内含全部样式、
脚本、着色器和一段内嵌的环境音乐，下载后双击即可离线运行，也能直接托管到
任意静态服务器（如 GitHub Pages）。

### 主题与概念

项目的核心表达是一句宣言：

> Freedom is coming. Information is power. Reclaim your human right to free
> expression.

整个作品围绕“黑暗中的光”这一隐喻展开——一座由数学分形实时生成的发光
“圣殿”悬浮在夜空里，缓慢自转、呼吸、变形，象征自由表达与信息的传播。
作品把五种不同的分形结构命名为五个**声音**（Voice），它们每十秒自动
“蜕变”一次，也可以由你亲手“绽放”切换。

### 体验流程

1. **开场幕布（The Transmission）** — 页面首先呈现一段宣言短片：
   标题与主旨逐行浮现，点击 / 触摸 / 按任意键即可进入，或等待约 5 秒自动淡出。
2. **黎明（Dawn）** — 幕布揭开后，场景辉光从近乎全黑逐渐增强（约 8 秒），
   如同曙光降临，呼应“Freedom Is Coming”。
3. **主场景** — 发光分形在星空中缓转，五种“声音”轮流显现；
   雕塑表面有一道暖色“广播波”缓慢向外游走；双击或按 `b` 会绽放出一阵光脉冲，
   切换到下一个声音。
4. **呼吸模式** — 按 `space` 隐藏全部界面，只留光和雕塑。

### 视觉与声音设计

- **调色**：深靛蓝 → 紫罗兰 → 金色的渐变材质，配合暖色主光与冷色补光；
- **景深层次**：背景是两层缓缓闪烁的星空与微噪星云，近处有带真实遮挡关系的
  3D 尘埃光点（只出现在“雕塑之前”的空间），整体画面由深到浅层次分明；
- **动态光**：开场黎明渐亮、每个声音到来时的光脉冲、表面广播波、
  以及画面边缘 9 秒周期的轻微呼吸暗角；
- **音乐**：内嵌一段环境配乐（默认开启）。受浏览器自动播放策略限制，
  首次进入后需点击或按任意键一次即可播放。

### 技术实现

- **渲染**：WebGL + 光线步进（ray-marching）片元着色器，逐像素实时计算
  五种符号距离场（SDF）：Mandelbulb、Menger 海绵、Sierpinski 四面体、
  Trinity Bulb 与 Urchin；形态切换时在两个距离场之间按进度混合，并对混合场
  重新缩放以保证步进稳定；
- **性能自适应**：启动时以低分辨率“热身”，依据实测帧时间逐帧平滑升降清晰度；
  GPU 看门狗在帧时间异常时自动降分辨率，避免驱动超时；形态蜕变期间自动
  预留像素余量（约 55% 分辨率），保证切换过程依旧流畅；
- **渲染加速**：主循环加入“包围球”加速——打不中雕塑的背景射线直接跳过
  上百步的空白行进，星空的像素几乎零开销；
- **输入**：指针 / 触摸拖拽旋转、滚轮或双指缩放、键盘（`space`、`b`、`m`、方向键）；
- **无障碍与偏好**：系统开启“减少动态效果”（prefers-reduced-motion）时自动
  跳过幕布、关闭呼吸暗角与冗余动画；URL 追加 `?lite=1` 进入低分辨率轻量模式，
  适合较弱设备。

### 文件结构

| 文件 | 说明 |
|------|------|
| `index.html` | 全部代码与资源（约 6.5 MB，含内嵌音轨的 base64） |
| `README.md` | 项目文档 |

---

## 操作说明

- **拖拽 / 触摸** — 旋转视角，环绕雕像
- **滚轮 / 双指缩放** — 拉近拉远，向深处潜入
- **`space`（空格）** — 呼吸模式，隐藏全部界面
- **`b` 键 / 双击 / 双击触摸** — 绽放，切换到下一个“声音”
- **`m` 键** — 背景音乐开关
- **方向键** — 平移视角

> 注意：浏览器会拦截音频自动播放。首次进入页面后，**点击或按任意键一次**即可开启背景音乐；若声音尚未启动，左下角会显示提示。

URL 末尾追加 `?lite=1` 可启用低分辨率轻量模式，适合较弱的设备。

---

**本项目修改自 [MiaAI-Lab/Ox-Alpha-Beutiful-HTML](https://github.com/MiaAI-Lab/Ox-Alpha-Beutiful-HTML)，由 Ox Alpha 生成。**
