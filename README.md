# Voice Design 提示词指南（中文）

*English: a practical Chinese guide to ElevenLabs Voice Design prompts — the format, the vocabulary, the traps, and what to do when a voice sounds different after you switch models.*

你描述一个声音，它给你造出来。听起来简单，实际上一大半的人卡在同一个地方：**提示词写得不像提示词**——用的是自己顺口的词，而不是模型认得的词。

这份指南讲三件事：

1. 提示词按什么骨架写，每个位置该填什么；
2. 哪些词是模型认的、哪些词是坑；
3. 换了合成模型之后，同一个嗓子听起来变了味，怎么一步步往回拉。

> **关于来源**：本文是整理自 ElevenLabs 官方 Voice Design 文档的中文教程，**不是官方文档的翻译转载**，措辞和结构都按中文习惯重写过。
> 官方原文：[Voice Design](https://elevenlabs.io/docs/eleven-creative/voices/voice-design)
> 第 8、9 节是官方文档里没有的，来自实际项目里的踩坑记录。

---

## 目录

- [1. 什么时候该用 Voice Design](#1-什么时候该用-voice-design)
- [2. 标准提示词骨架](#2-标准提示词骨架)
- [3. 逐个字段拆开讲](#3-逐个字段拆开讲)
- [4. 中英对照词表](#4-中英对照词表)
- [5. 三个最容易踩的坑](#5-三个最容易踩的坑)
- [6. 预览文本怎么写](#6-预览文本怎么写)
- [7. 两个参数：Loudness 与 Guidance Scale](#7-两个参数loudness-与-guidance-scale)
- [8. 换了模型，声音变味了怎么办](#8-换了模型声音变味了怎么办)
- [9. 提交之前的自检清单](#9-提交之前的自检清单)
- [10. 参考与许可](#10-参考与许可)

---

## 1. 什么时候该用 Voice Design

**适合：**

- 声音库里找不到你要的嗓子，需要现造一个；
- 想快速试很多方向，出一个大致对味的就继续调；
- 角色音、旁白、虚拟助手这类可以有明确人设的声音。

**不适合：**

- 你已经有一个能用的真人声音克隆。官方的 Professional Voice Clone 在音质和一致性上都更好，声音库里有合适的就应该优先用它，而不是自己造一个“差不多”的。
- 你只是想换个语气说话。声音一旦生成并保存，之后怎么说话跟提示词就没关系了——那是音频标签和参数的事。这条很关键，第 8 节会展开。

**机制上的几个数字：**

- 每次生成给你 **3 个候选**；
- 只按**预览文本的字数**扣一次费，三个候选算一次；
- 挑一个保存，会占用一个声音位。

---

## 2. 标准提示词骨架

官方推荐的骨架是四行：

```
Native <语言>. <性别>, <年龄段>. <音质等级>.
Persona: <2–5 个词>.
Emotion: <2–3 个形容词>.
<1–2 句话描述音色、语速、表达方式>
```

照着填一个：

```
Native English, neutral American accent. Female, in her early 40s. Excellent audio quality.
Persona: audiobook narrator. Emotion: composed, warm, curious.
Clear, even timbre with natural breath, recorded in a quiet room.
Speaks at a conversational pace, pausing briefly between sentences.
```

几点说明：

- **换行只是为了给人看**，模型不靠行来理解结构。真正要紧的是这四类信息别缺：语言/性别/年龄/音质、人设、情绪、音色和语速的描述。
- **写得细不是错**。官方明确说，描述越具体、越细，结果越准。
- 但**短提示词也能用**。如果你要的是一个中性、不挑内容的嗓子，一句 `A calm male narrator` 可能就够了。要不要写细，取决于你有多想要某个具体的声音。

---

## 3. 逐个字段拆开讲

### 3.1 语言——第一句就要写

格式是 `Native <语言>`，而且**要连地区变体一起写**。

不写语言的后果，对中文嗓子尤其明显：模型会自己去猜一个语言底子，猜偏了，说中文的调子就不对——听起来“像老外在说中文”或者“腔调怪怪的”，但你很难说出具体哪里怪。

中文可以这样写：

```
Native Mandarin Chinese, standard mainland Mandarin.
```

要某个地区口音就写清楚，比如 `Mandarin Chinese with a slight Sichuan accent`。

### 3.2 音质等级——单独一句

可用的档位（官方的原词，建议照抄）：

| 档位 | 英文原词 |
| --- | --- |
| 一般 | `Ok quality` |
| 好 | `Good quality` |
| 很好 | `Very good quality` |
| 优秀 | `Excellent quality` |
| 录音棚 | `Studio quality` |
| 广播级 | `Broadcast quality` |

也可以直接写一句 `perfect audio quality` 或 `studio-quality recording`。

**反过来**：如果你就是要低音质的效果（电话、老录音、监控回放），不要写档位，改成明确要差：

- `Low-fidelity audio`
- `Poor audio quality`
- `Sounds like a voicemail`
- `Muffled and distant, like on an old tape recorder`

**一个警告**：如果你的嗓子本身很特殊、很刁钻，加音质词有可能反而让提示词整体的准确度下降。音质和“像不像”之间是要取舍的。

### 3.3 年龄——给范围，别给精确数字

写“大约 24 岁”和写“in their late 20s”，出来的是两个不同的声音。年龄是**听起来几岁**最直接的一根杠杆。

好用的写法：

```
adolescent male / adolescent female
young adult / in their 20s / early 30s
middle-aged man / woman in her 40s
elderly man / older woman / man in his 80s
```

两点提醒：

- **它管“老成”，不管“音高”。** 想把声音压低，主要靠音色词（`low-pitched` / `deep`），年龄往上抬只是辅助。
- **它是可以过头的。** 同一把嗓子上，年龄往上抬两档会明显显老、发闷，抬一档刚好（实际使用反馈，不是严格对比实验）。所以别一次跳太多，一档一档试。

### 3.4 音色——用词表里的词

音色说的是声音本身的物理质感（音高、共鸣、粗糙度），跟情绪、态度是两回事。

常用词：

```
deep / low-pitched        低沉
smooth / rich             平滑、厚实
gravelly / raspy          沙哑、糙
nasally / shrill          鼻音重、尖
airy / breathy            气声
booming / resonant        浑厚、有共鸣
light / thin              轻、薄
warm / mellow             温暖、柔
tinny / metallic          金属感、发闷
```

**不要自创词。** 比如想表达“中低音区”，词表里就是 `deep` 或 `low-pitched`，写 `medium-deep tone` 属于自创——模型不一定会理解成你要的意思，尤其在你要的是“往下压音高”这种精确操作时。

### 3.5 性别——可以不写身份，直接描述声音

除了 `male` / `female` / `gender-neutral`，也可以只描述声音本身的特征：

```
A lower-pitched, husky female voice
A masculine male voice, deep and resonant
A neutral gender — soft and mid-pitched
```

### 3.6 口音——这里最容易翻车

这一栏有三条硬规矩：

1. **你想说的是“语调”，千万别写 `accent`。**
   中文里我们说“他说话有口音”，英语里 accent 指的是**地区方言**。你要是想调的是重音位置、语调起伏，写 `accent` 会让模型真的给你换一个方言。想调语调就写 `intonation`、`emphasis`、`delivery`。

2. **用 `thick` 比用 `strong` 稳。**
   描述口音有多重，`thick French accent` 比 `strong French accent` 出来的结果更一致。

3. **别写 `foreign`、`exotic`。**
   太含糊，结果飘。

清楚的写法长这样：

```
a middle-aged man with a thick French accent
a young woman with a slight Southern drawl
an old man with a heavy Eastern European accent
a cheerful woman speaking with a crisp British accent
a younger male with a soft Irish lilt
an authoritative voice with a neutral American accent
```

口音最好**和年龄、语速、音色一起写**，单写口音很容易被别的特征盖掉。

### 3.7 语速——写清楚快慢，还要写清“感觉”

```
speaking quickly / at a fast pace
at a normal pace / speaking normally
speaking slowly / with a slow rhythm
deliberate and measured pacing
drawn out, as if savoring each word
with a hurried cadence, like they're in a rush
relaxed and conversational pacing
rhythmic and musical in pace
erratic pacing, with abrupt pauses and bursts
even pacing, with consistent timing between words
staccato delivery
```

如果语速会变，最好**写清楚在哪变、为什么变**，比如 `accelerates when excited`。

### 3.8 Persona（人设）——2 到 5 个词

不是写性格，是写**这个人是谁**。一个职业、一个身份、一个处境都行：

```
Persona: quiet late-night companion.
Persona: veteran radio host.
Persona: tired but patient nurse.
```

人设的作用是给模型一个整体的“演法”。同一组音色描述，配上不同的人设，出来的气质会不一样。

### 3.9 Emotion（情绪）——2 到 3 个形容词

```
Emotion: gentle, steady, attentive.
Emotion: excited, nervous, hopeful.
```

**不要写否定句。** 这条在情绪和音色上尤其明显：模型对“要什么”的服从度，远高于对“不要什么”的服从度。

- ✗ `not too loud`
- ✓ `quiet`, `soft-spoken`, `calm presence`
- ✗ `not overly dramatic`
- ✓ `restrained`, `understated`, `even-toned`

---

## 4. 中英对照词表

| 属性 | 可用的英文词 |
| --- | --- |
| 年龄 | young, younger, adult, old, elderly, in his/her 40s |
| 口音 | "thick" Scottish accent, "slight" Asian-American accent, Southern American accent |
| 性别 | male, female, gender-neutral, ambiguous gender |
| 音色 / 音质 | deep, warm, gravelly, smooth, shrill, buttery, raspy, nasally, throaty, harsh, robotic, ethereal |
| 语速 | normal cadence, fast-paced, quickly, slowly, drawn out, calm pace, natural/conversational pace |
| 音质等级 | perfect audio quality, audio quality is 'ok', poor audio quality |
| 人设 / 职业 | pirate, businessman, farmer, politician, therapist, ogre, godlike being, TV announcer |
| 情绪 | energetic, excited, sad, emotional, sarcastic, dry |
| 音高 | low-pitched, high-pitched, normal pitch |

> 同一个描述换个说法，结果可能不同。比如 `Perfect audio quality` 和 `the audio quality is perfect`，效果有时会有差别。官方自己也建议多换说法试。

---

## 5. 三个最容易踩的坑

### 坑一：把“语调”写成“accent”

参见 [3.6](#36-口音这里最容易翻车)。症状是：你只想让声音说话更有起伏，结果出来一个带方言的嗓子。

### 坑二：加了效果词

`reverb`、`echo`、`phone`、`tape` 这类词——**即使你只是想在描述里提一嘴**，也可能把音质拉垮。

要电话感、老录音感，用 3.2 里那几句专门的写法（`Sounds like a voicemail`、`Muffled and distant...`），不要写 `reverb`。

### 坑三：不写语言

第一句不写 `Native <语言>`，模型就自己猜。猜对了没事，猜错了就是“说不出哪里怪”。

---

## 6. 预览文本怎么写

预览文本是**它的台词**。同一把嗓子，念不同的话，听起来能差出一截。

规则只有一条：**预览文本的情绪要和提示词一致，不能打架。**

- 提示词写“平静、内省、带一点日式口音的年轻女声”，预览文本却写“嘿！我真是受够你把这地方搞成什么样了！！”——模型会努力去调和这个矛盾，出来的声音多半会变形。
- 换成 `It's been quiet lately... I've had time to think, and maybe that's what I needed most.` 就对了。

两条经验：

1. **长一点比短一点稳。** 短句容易突兀、不稳定，尤其是你在试“语气”这种细微的东西时。给一整个句子甚至一小段，效果更好。
2. **可以带音频标签**，比如 `[laughs]`、`[sighs]`、`[exhales]`。生成的时候它们会指导表演，而且不算“效果词”。

---

## 7. 两个参数：Loudness 与 Guidance Scale

### Loudness（响度）

控制预览和最终保存的声音的音量。一般不用动。

### Guidance Scale（提示词贴合度）

决定模型有多“听话”。

| 取值 | 效果 | 什么时候用 |
| --- | --- | --- |
| 高 | 严格贴着提示词走；但如果提示词很特殊，音质可能变差 | 口音、音色必须准的时候 |
| 低 | 模型更放得开，表演感和音质更好，但可能不太听话 | 你要的是“好听、自然”，提示词只是方向 |

官方自己给的示例里，角色音大多落在 **20%–40%** 之间。口音或音色一跑偏，先往高调；声音发闷、发僵，先往低调。

---

## 8. 换了模型，声音变味了怎么办

这一节是官方文档里没有的。

### 8.1 先分清两件事：提示词管“造”，模型管“念”

这是整份指南最重要的一句话。

- **提示词只在生成的那一刻起作用。** 它决定一个声音的“长相”：音高、音色、口音、说话习惯。
- 生成之后保存下来的是一个**声音 ID**。此后它念什么内容、用什么情绪，由合成模型、参数和音频标签决定，**和提示词再没有关系**。

由此推出两个很实际的结论：

1. **只想换模型、不想换声音** → 别动提示词。改了也不会让新模型更像旧模型。
2. **新模型上声音变了味** → 改提示词对已有的那个声音没用，**必须用新提示词重新生成一个声音**，才能把“变年轻、变高了”这类变化拉回来。

具体到这次实测：把 v3 上已经生成好的声音直接放到 v4 上念，声音明显年轻了好几岁、音调也高——问题出在「**旧声音 + 新模型**」，不在旧提示词写得好不好。

### 8.2 症状：换了模型，同一个嗓子年轻了好几岁、音调也高了

这不是错觉。不同合成模型对同一把嗓子的演绎本来就会有差异。如果新版听上去偏年轻、偏高，按下面的顺序排查——**从影响最大的往下改**：

**① 没写语言。**

官方骨架第一句就是 `Native <语言>`。对中文嗓子尤其要紧：不写，模型可能给你一个偏英文底子的嗓子，说中文的调子就会怪。

**② 没写音质等级。**

骨架里要求有一句，比如 `Excellent audio quality`。缺了它，模型不知道你要的是干净的高保真还是随手的录音。

**③ 音高词不在词表里。**

官方词表里对应“中低音”的是 `low-pitched` 或 `deep`。`medium-deep tone` 这种写法是自创的。想往下压音高这种精确操作，**一定要用词表里的原词**。

**④ 年龄写死了精确数字——但它不是“变年轻”的原因。**

这里要先分清一件事：这次“年轻了好几岁”，**直接原因是把 v3 上已经生成好的旧声音直接拿到 v4 上念**（同一个声音，换模型演绎，v4 读得更年轻、更高），不是提示词里的年龄数字写出来的。

年龄仍然好用，但它是**微调用的，不是拿来对冲的**：

- 写精确数字会把这根杠杆钉死，只能整段重写；
- 往上抬要**一档一档试**：实际使用中抬两档就偏老、发闷，抬一档刚好；
- 压音高主要还是靠 `low-pitched` 这类音色词，别指望把年龄写大来撑低音。

**⑤ 有否定句。**

`not too loud`、`not overly dramatic`——模型对“不要什么”的服从度远不如“要什么”。改成正面说法：

| 否定 | 改成 |
| --- | --- |
| not too loud | quiet / soft-spoken |
| not overly dramatic | restrained / understated |

**⑥ 少了 Persona 和 Emotion 两行。**

骨架要求 Persona 2–5 个词、Emotion 2–3 个形容词。缺这两行，模型只能靠自己猜整体气质。

### 8.3 改前 / 改后对照

用一个和本案例无关的例子（深夜电台主持人）演示这六处怎么改。改前那段是随手写的，几个问题都占全了：

```
A middle-aged male voice for a late-night radio show, medium-deep pitch, around age 45.
Warm and relaxed, but not too casual. Speaks at a moderate pace with clear articulation.
```

按骨架重写之后：

```
Native English, neutral American accent. Male, mid 40s. Excellent audio quality.
Persona: late-night radio host. Emotion: calm, welcoming, attentive.
Low-pitched, rounded timbre, recorded close to the microphone with no room noise.
Speaks at a relaxed, even pace, leaving a short pause between ideas and landing softly on
the last few words of each sentence.
```

对照着看改了哪六处：

| # | 改动 | 为什么 |
| --- | --- | --- |
| 1 | 加 `Native English, neutral American accent` | 不给语言底子，模型自己猜，口音容易飘 |
| 2 | 加 `Excellent audio quality` | 骨架要求的音质等级 |
| 3 | `medium-deep pitch` → `Low-pitched, rounded` | 用词表原词，模型才认 |
| 4 | `around age 45` → `mid 40s` | 精确数字钉死杠杆；改成范围，留出微调余地 |
| 5 | `but not too casual` → `calm, welcoming` | 否定改肯定 |
| 6 | 补 `Persona:` 和 `Emotion:` 两行 | 骨架要求，帮模型定整体气质 |

### 8.4 这几样**不算**问题，别乱删

- **写得长是好事。** 官方明说越细越准。一整段描述是好的写法，不要为了“简洁”硬砍。
- **比喻不犯规。** 官方自己的示例提示词里就有比喻（比如把声音比作某种人）。
- **对着词表写的表达可以留。** 比如 `speaks at a conversational pace` 这种，是照词表来的，保留。

---

## 9. 提交之前的自检清单

复制走，每次生成前过一遍：

- [ ] 第一句是 `Native <语言>`，并且写了地区/方言变体
- [ ] 有一句明确的音质等级（或者明确要低音质）
- [ ] 年龄写的是范围，不是精确数字
- [ ] 音色、音高用的词都在词表里，没有自创
- [ ] 想说的是“语调”时，没有写成 `accent`
- [ ] 没有 `reverb` / `echo` / `phone` / `tape` 这类效果词
- [ ] 所有否定句都改成了肯定说法
- [ ] `Persona:` 和 `Emotion:` 两行都在
- [ ] 预览文本的情绪和提示词一致
- [ ] Guidance Scale 和嗓子的难度匹配（跑偏往高调，发僵往低调）

---

## 10. 参考与许可

- 官方文档：[ElevenLabs · Voice Design](https://elevenlabs.io/docs/eleven-creative/voices/voice-design)
- 本文为中文整理与原创补充，不是官方文档的翻译转载；官方内容以原链接为准。
- 可直接粘贴使用的完整示例提示词见 [examples.md](examples.md)。
- 本文以 [CC BY 4.0](LICENSE) 许可发布，转载注明出处即可。

ELEVENLABS 是其各自所有者的商标。本项目为非官方社区教程。
