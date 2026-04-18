# 朝早流程助手：修改教学文档

呢份文档系畀将来嘅你自己睇嘅。目标唔系教你学编程，而系等你想改嘢嗰阵，**知道去边度改、改边几行、边啲唔好乱掂**。

---

## 一、先记住整体结构

你个 `index.html` 大致分 3 部分：

### 1. 画面（HTML）
负责按钮、标题、计时器、目前播放文字。

你通常**唔需要点改**，除非你想改按钮字、提示字、或者画面上显示啲咩。

### 2. 样式（CSS）
负责颜色、大细、圆角、间距。

你通常**唔需要点改**，除非你想改外观。

### 3. 逻辑（JavaScript）
真正重要嘅系呢部分。你平时会改嘅，主要系：

- `const steps = [...]`
- `const musicLibrary = {...}`
- 某啲提示文字

---

## 二、你平时最常改嘅 2 个区域

# A. 流程内容：`const steps = [...]`

每一步都系一个对象，例如：

```javascript
{ name: "刷牙", duration: 6 * 60, speakText: "Brush teeth" }
```

或者有歌嘅步骤：

```javascript
{ name: "涂防晒 + 梳头 + 影相", duration: 8 * 60, category: "game", speakText: "Put on sunscreen, comb hair and take photos" }
```

### 每个字段意思

- `name`
  - 画面显示嘅中文名
  - 例如：`"刷牙"`

- `duration`
  - 呢一步几多秒
  - 例如：`6 * 60` 就系 6 分钟

- `speakText`
  - 英文语音会读出呢句
  - 例如：`"Brush teeth"`

- `category`
  - 呢一步要播边个歌单分类
  - 例如：`"anime"`、`"game"`
  - **冇写就唔会播歌**

---

# B. 歌单内容：`const musicLibrary = {...}`

例如：

```javascript
const musicLibrary = {
  anime: [
    "audio/anime/1.mp3",
    "audio/anime/2.mp3"
  ],
  game: [
    "audio/game/1.mp3",
    "audio/game/2.mp3"
  ]
};
```

### 结构意思

- `anime`、`game`
  - 呢啲系歌单分类名
  - 要同 `steps` 里面嘅 `category` 对得上

- 数组里面每一行
  - 系一首歌嘅路径
  - 路径一定要同 GitHub / 本地文件夹结构一致

---

## 三、最常见修改：直接照抄

# 1. 想改某一步个中文显示

例如将：

```javascript
{ name: "刷牙", duration: 6 * 60, speakText: "Brush teeth" }
```

改成：

```javascript
{ name: "刷牙 + 整牙线", duration: 6 * 60, speakText: "Brush teeth" }
```

### 会影响咩？
- 只会影响画面显示
- **唔会影响功能**

---

# 2. 想改某一步时间

例如将 6 分钟改做 8 分钟：

```javascript
{ name: "刷牙", duration: 8 * 60, speakText: "Brush teeth" }
```

### 规则
- `几分钟 * 60`
- 例如：
  - 3 分钟 = `3 * 60`
  - 15 分钟 = `15 * 60`

---

# 3. 想改英文语音内容

例如：

```javascript
speakText: "Brush teeth"
```

改成：

```javascript
speakText: "Time to brush your teeth"
```

### 会影响咩？
- 会影响英文语音读出内容
- **唔影响其他功能**

---

# 4. 想新增一个步骤

例如你想喺“洗面”后面加“洗鼻”：

```javascript
{ name: "洗鼻", duration: 3 * 60, speakText: "Wash nose" }
```

如果呢一步想播歌：

```javascript
{ name: "洗鼻", duration: 3 * 60, category: "anime", speakText: "Wash nose" }
```

### 注意
- 每一步之间要有逗号 `,`
- 最后一行后面可以唔加，但中间行一定要有

---

# 5. 想删除一个步骤

直接删咗嗰一整行对象就得。

例如删：

```javascript
{ name: "拖地", duration: 4 * 60, speakText: "Mop the floor" }
```

### 注意
- 删除后，上面一行同下面一行嘅逗号要正常

---

# 6. 想令某一步开始播歌

例如原本系：

```javascript
{ name: "屙屎", duration: 10 * 60, speakText: "Use the bathroom" }
```

改成：

```javascript
{ name: "屙屎", duration: 10 * 60, category: "anime", speakText: "Use the bathroom" }
```

### 条件
- `category` 一定要对应到 `musicLibrary` 入面已有嘅分类

---

# 7. 想令某一步唔播歌

删走 `category` 就得。

例如：

由：

```javascript
{ name: "屙屎", duration: 10 * 60, category: "anime", speakText: "Use the bathroom" }
```

改成：

```javascript
{ name: "屙屎", duration: 10 * 60, speakText: "Use the bathroom" }
```

---

# 8. 想加歌

去 `musicLibrary` 对应分类入面加一行。

例如：

```javascript
anime: [
  "audio/anime/1.mp3",
  "audio/anime/2.mp3",
  "audio/anime/3.mp3"
]
```

加到：

```javascript
anime: [
  "audio/anime/1.mp3",
  "audio/anime/2.mp3",
  "audio/anime/3.mp3",
  "audio/anime/4.mp3"
]
```

### 同时要做嘅事
你真系要喺文件夹入面有：

```text
audio/anime/4.mp3
```

如果代码有、文件冇，就播唔到。

---

# 9. 想减歌

喺 `musicLibrary` 删除对应一行就得。

例如删：

```javascript
"audio/anime/4.mp3",
```

如果文件夹里仲有 `4.mp3`，可以唔理；
只要 `musicLibrary` 冇引用，程式就唔会播到佢。

---

# 10. 想新增一个新歌单分类

例如想加 `drama`：

## 第一步：喺 `musicLibrary` 加分类

```javascript
drama: [
  "audio/drama/1.mp3",
  "audio/drama/2.mp3"
]
```

## 第二步：喺文件夹加歌

```text
audio/drama/1.mp3
audio/drama/2.mp3
```

## 第三步：喺步骤度引用

```javascript
{ name: "食早餐", duration: 20 * 60, category: "drama", speakText: "Eat breakfast" }
```

---

## 四、而家播放紧边首歌：点解会显示文件名

而家程式显示嘅系：

```text
目前播放：1.mp3
```

因为而家系直接由路径抽文件名出来显示。

### 好处
- 加歌唔使额外写标题
- 最省事

### 代价
- 你见到嘅系 `1.mp3` 呢种名
- 唔系正式歌名

### 如果将来想令显示更好睇
最简单方法系直接改文件名，例如：

```text
audio/anime/Ultraman Theme.mp3
```

咁画面就会显示：

```text
目前播放：Ultraman Theme.mp3
```

---

## 五、真随机播歌：而家逻辑点运作

而家呢版唔系“先 shuffle 一次再顺住播”，而系：

- 每次要播下一首
- 都喺当前分类入面重新 random 抽
- 但避免同上一首完全一样

### 所以会出现嘅情况
可能：
- 2.mp3
- 5.mp3
- 1.mp3
- 2.mp3

呢个系正常。

### 唔会出现嘅情况
通常唔会：
- 2.mp3
- 2.mp3

因为已经做咗“避免同上一首一样”。

---

## 六、边啲可以放心改，边啲最好唔好乱掂

# 可以放心改

### 1. `steps` 里面呢啲字段
- `name`
- `duration`
- `speakText`
- `category`

### 2. `musicLibrary` 里面嘅歌路径

### 3. 画面上一啲提示文字
例如：
- “目前未播放音樂”
- “建議時間...”

---

# 最好唔好乱掂

### 1. 变量名
例如：
- `currentIndex`
- `timeLeft`
- `currentCategory`
- `currentTrackSrc`
- `lastTrackSrc`

### 2. function 名
例如：
- `pickRandomTrack`
- `playCurrentTrack`
- `playStepAudio`
- `pauseEverything`
- `startCurrentStepSequence`

### 3. 结构符号
例如：
- `{ }`
- `[ ]`
- `( )`
- 逗号 `,`
- 引号 `" "`

### 4. HTML 元素 id
例如：
- `id="bgm"`
- `id="stepName"`
- `id="nowPlaying"`

改咗呢啲，功能好容易壞。

---

## 七、最常见报错原因

# 1. 逗号漏咗
例如：

```javascript
{ name: "刷牙", duration: 6 * 60 }
{ name: "洗面", duration: 5 * 60 }
```

中间冇逗号，咁就会报错。

正确：

```javascript
{ name: "刷牙", duration: 6 * 60 },
{ name: "洗面", duration: 5 * 60 }
```

---

# 2. 路径写错
例如代码写：

```javascript
"audio/anime/4.mp3"
```

但文件实际叫：

```text
audio/anime/04.mp3
```

咁就播唔到。

---

# 3. 分类名对唔上
例如 step 写：

```javascript
category: "Anime"
```

但 `musicLibrary` 写：

```javascript
anime: [...]
```

大小写唔同，咁就搵唔到歌单。

正确应该完全一样。

---

# 4. 文件上传咗，但 `musicLibrary` 冇加
咁程式唔会知道有呢首歌。

---

# 5. 代码改完但网站冇更新
通常原因：
- 改错文件（要改 `index.html`）
- GitHub Pages 仲未刷新
- 浏览器缓存

### 处理方法
- 确认改嘅系 `index.html`
- 等 1–3 分钟
- 用无痕模式开网站

---

## 八、GitHub 更新流程（最实用）

如果你用 GitHub Desktop：

### 改代码后
1. 存档
2. 去 GitHub Desktop
3. 睇 Changes
4. 写一句 summary
   - 例如：`update morning steps`
5. 撳 `Commit to main`
6. 撳 `Push origin`
7. 等 1–3 分钟
8. 去网站刷新

---

## 九、你以后最常用嘅“模板”

# 模板 1：新增一个无音乐步骤

```javascript
{ name: "洗鼻", duration: 3 * 60, speakText: "Wash nose" }
```

# 模板 2：新增一个有音乐步骤

```javascript
{ name: "整理出门物品", duration: 5 * 60, category: "game", speakText: "Prepare things to go out" }
```

# 模板 3：喺 anime 分类加一首歌

```javascript
"audio/anime/15.mp3"
```

# 模板 4：新增一个分类

```javascript
musicLibrary = {
  anime: [...],
  game: [...],
  drama: [
    "audio/drama/1.mp3",
    "audio/drama/2.mp3"
  ]
}
```

然后步骤咁写：

```javascript
{ name: "食早餐", duration: 20 * 60, category: "drama", speakText: "Eat breakfast" }
```

---

## 十、最懒人原则（你以后跟住呢个就得）

### 想改流程
→ 去 `steps`

### 想改歌
→ 去 `musicLibrary`

### 想改语音
→ 改 `speakText`

### 想改显示中文
→ 改 `name`

### 想停播歌
→ 删 `category`

### 想开播歌
→ 加 `category`

---

## 十一、最后一句提醒

你以后想改嘢，**先改一小部分，存档，测试**。

唔好一次过：
- 改 10 个步骤
- 加 20 首歌
- 再改 5 条逻辑

因为一壞，你会唔知边度出事。

最稳方法：
1. 改 1 处
2. 测试
3. 再改下一处

---

如果将来你仲想加新功能，例如：
- 最近 3 首唔准重复
- 新增分类
- 更复杂嘅显示歌名
- 手机版更稳播放

你就拎住呢份文档，再问我就得。

