# Ox-Alpha-Beutiful-HTML — AETHER

> **Source / 来源**
>
> This project is modified from [MiaAI-Lab/Ox-Alpha-Beutiful-HTML](https://github.com/MiaAI-Lab/Ox-Alpha-Beutiful-HTML).
> 本项目修改自 [MiaAI-Lab/Ox-Alpha-Beutiful-HTML](https://github.com/MiaAI-Lab/Ox-Alpha-Beutiful-HTML)。

---

## About · 项目简介

**English**

AETHER — Freedom Is Coming is a single-file, zero-dependency, offline-capable
WebGL interactive artwork. Everything lives inside one `index.html`: styles,
scripts, the shader, and the embedded ambient score. Double-click the file to
run it, or host it on any static server (such as GitHub Pages).

Its core message: *Freedom is coming. Information is power. Reclaim your human
right to free expression.*

The piece embodies "light in the dark": a luminous cathedral generated in real
time from mathematical fractals, floating in a night sky — slowly rotating,
breathing, and morphing between five "voices" every ten seconds, or whenever
you call one forth yourself.

**简体中文**

AETHER — Freedom Is Coming 是一个单文件、零依赖、可离线运行的浏览器 WebGL
交互艺术作品。全部内容都封装在同一个 `index.html` 里：样式、脚本、着色器与
内嵌环境音乐。双击文件即可运行，也可托管到任意静态服务器（如 GitHub Pages）。

它的核心表达是：*Freedom is coming. Information is power. Reclaim your human
right to free expression.*（自由将至。信息即力量。收回你自由表达的人权。）

作品用“黑暗中的光”作为隐喻：一座由数学分形实时生成的发光圣殿悬浮于夜空，
缓慢旋转、呼吸，并每十秒在五个“声音”之间蜕变——你也可以亲手召唤下一个声音。

---

## The Five Voices · 五个声音

| Voice（声音） | Technical form（数学形态） | Meaning（含义） |
|---------------|----------------------------|-----------------|
| THE LAMP | Mandelbulb | 思想的灯火 |
| THE CATHEDRAL | Menger Cathedral | 开放的殿堂 |
| THE FLAME | Sierpinski Flame | 自由之火 |
| THE TRIAD | Trinity Bulb | 寻求 · 接收 · 传递 |
| THE BROADCAST | Urchin | 向四方发送的信号 |

**English**

The five fractal forms are presented as five "voices". Each arrival of a new
voice is announced by a soft pulse of light and a broadcast wave traveling
across the sculpture's surface.

**简体中文**

五种分形结构以五个“声音”的面貌呈现。每个新声音到来时，都会伴随一阵柔和的
光脉冲，以及一道沿着雕塑表面向外游走的“广播波”。

---

## Experience · 体验流程

**English**

1. **The Transmission (opening veil)** — a short manifesto sequence shows the
   title and message line by line. Enter with a click / tap / any key, or wait
   about 5 seconds for it to fade on its own.
2. **Dawn** — after the veil lifts, the scene's glow rises from near-dark to
   full over about 8 seconds, like light arriving.
3. **Main scene** — the luminous fractal drifts and breathes among the stars;
   the five voices transmute on their own; double-click or press `b` to bloom
   into the next voice with a flare of light.
4. **Zen mode** — press `space` to hide the whole interface and keep only the
   light and the sculpture.

**简体中文**

1. **开场幕布（The Transmission）** —— 一段简短的宣言：标题与主旨逐行浮现。
   点击 / 触摸 / 按任意键进入，或等待约 5 秒自动淡出。
2. **黎明（Dawn）** —— 幕布揭开后，场景辉光在约 8 秒内从近乎全黑逐渐增强，
   如同光芒抵达。
3. **主场景** —— 发光分形在星空中漂移与呼吸；五个声音自动蜕变；
   双击或按 `b` 键可绽放出一阵光，切换到下一个声音。
4. **呼吸模式（Zen）** —— 按 `space` 隐藏全部界面，只留下光与雕塑。

---

## Visual & Sound Design · 视觉与声音设计

**English**

- Palette: deep indigo → violet → gold materials, lit by a warm key light and a
  cool fill light.
- Depth: two layers of twinkling stars behind; 3D dust motes in the space
  *between* camera and sculpture (so they never cover it); clear far-to-near
  layering.
- Motion: the opening dawn, a soft pulse on each voice arrival, a slow
  "broadcast wave" traveling across the surface, and a gentle 9-second
  breathing vignette at the edges.
- Sound: an embedded ambient score, on by default. Because browsers block
  audio autoplay, tap or press any key once to start it.

**简体中文**

- 调色：深靛蓝 → 紫罗兰 → 金色的材质，以暖色主光与冷色补光照明。
- 景深：背后是两层闪烁的星空；镜头与雕塑之间的空间中漂浮着 3D 尘埃光点
  （因此不会遮挡雕塑），由远及近层次分明。
- 动态：开场黎明渐亮、每个声音到来时的柔光脉冲、沿表面缓慢游走的“广播波”、
  以及画面边缘 9 秒周期的轻微呼吸暗角。
- 声音：内嵌环境配乐，默认开启。受浏览器自动播放限制，点击或按任意键一次
  即可开始播放。

---

## Technical Implementation · 技术实现

**English**

- Rendering: WebGL ray-marching fragment shader that evaluates five signed
  distance fields (Mandelbulb, Menger sponge, Sierpinski tetrahedron, Trinity
  Bulb, Urchin) per pixel. During a transmutation, two fields are blended by
  progress, and the blended field is rescaled to keep the march stable.
- Adaptive performance: starts at low resolution as a "warm-up", then smoothly
  raises or lowers quality every frame based on measured frame times. A GPU
  watchdog lowers resolution automatically if frames stall, preventing driver
  timeouts. During morphs it reserves headroom (~55 % resolution) so switching
  stays smooth.
- March acceleration: a bounding-sphere test skips the long empty march for
  rays that never reach the sculpture — sky pixels cost almost nothing.
- Input: drag / touch to orbit, wheel or pinch to dive, keyboard (`space`,
  `b`, `m`, arrow keys).
- Accessibility: with `prefers-reduced-motion`, the veil is skipped and
  decorative animation is disabled. Append `?lite=1` for a lighter, lower
  resolution mode on weaker devices.

**简体中文**

- 渲染：WebGL 光线步进（ray-marching）片元着色器，逐像素计算五种符号距离场
  （Mandelbulb、Menger 海绵、Sierpinski 四面体、Trinity Bulb、Urchin）。
  形态切换时按进度混合两个距离场，并对混合场重新缩放以保证步进稳定。
- 自适应性能：启动时以低分辨率“热身”，随后根据实测帧时间逐帧平滑升降清晰度；
  GPU 看门狗在帧时间异常时自动降分辨率，避免驱动超时；蜕变期间预留约 55%
  分辨率的余量，保证切换过程流畅。
- 步进加速：主循环加入“包围球”测试，打不中雕塑的射线直接跳过漫长的空白行进
  —— 星空像素几乎零开销。
- 输入：拖拽 / 触摸旋转，滚轮或双指缩放，键盘（`space`、`b`、`m`、方向键）。
- 无障碍：开启系统“减少动态效果”（prefers-reduced-motion）时跳过幕布并关闭
  装饰动画；URL 追加 `?lite=1` 可在较弱设备上使用更轻、更低分辨率模式。

---

## Files · 文件结构

| File（文件） | Note（说明） |
|--------------|--------------|
| `index.html` | **EN:** the entire project, including the embedded score (~6.5 MB)<br>**中文：** 整个项目，含内嵌音轨（约 6.5 MB） |
| `README.md` | **EN:** this documentation<br>**中文：** 本文档 |

---

## Controls · 操作说明

**English**

- drag / touch — orbit the sculpture
- scroll / pinch — dive in and out
- `space` — zen (hide the interface)
- `b`, double-click / double-tap — bloom into the next voice
- `m` — toggle sound
- arrow keys — move the camera

**简体中文**

- 拖拽 / 触摸 —— 旋转视角，环绕雕塑
- 滚轮 / 双指缩放 —— 拉近拉远
- `space`（空格） —— 呼吸模式，隐藏界面
- `b` 键 / 双击 / 双击触摸 —— 绽放，切换到下一个声音
- `m` 键 —— 声音开关
- 方向键 —— 平移视角

> Browser autoplay policy: tap or press any key once to start the music — the
> prompt disappears as soon as the sound is playing.
> 浏览器会拦截音频自动播放：点击或按任意键一次即可开启音乐，提示会在声音真正
> 响起后自动消失。

---

**本项目修改自 [MiaAI-Lab/Ox-Alpha-Beutiful-HTML](https://github.com/MiaAI-Lab/Ox-Alpha-Beutiful-HTML)，由 Ox Alpha 生成。**
**This project is modified from [MiaAI-Lab/Ox-Alpha-Beutiful-HTML](https://github.com/MiaAI-Lab/Ox-Alpha-Beutiful-HTML) and was generated by Ox Alpha.**
