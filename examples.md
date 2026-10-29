# 可以直接粘贴的示例提示词

每个示例都是「提示词 + 预览文本」一组，按 [README](README.md) 里的骨架写的。
`Guidance Scale` 是按这把嗓子的难度给的建议值，不是必须。

---

## 1. 中文男声 · 深夜陪伴

适合：陪伴类应用、夜间电台、读书。

```
Native Mandarin Chinese, standard mainland Mandarin. Male, late 20s. Excellent audio quality.
Persona: patient companion. Emotion: calm, warm, attentive.
Low-pitched, warm timbre with a soft edge, recorded close to the microphone with no room noise.
Speaks at an unhurried, even pace with soft emphasis at the end of sentences.
```

**预览文本**

```
还没睡啊。灯先别关，我再陪你坐一会儿。今天不用说什么，就这样安静着，也挺好的。
```

**Guidance Scale**：35%

**说明**：`standard mainland Mandarin` 别省。想更沉一点，**先动音色词**（比如把 `warm` 换成 `resonant`，或再加一个 `deep`）；年龄最多挪一档，别一次跳两级——写过头会显老、发闷（实际反馈）。

---

## 2. 中文女声 · 播客旁白

适合：播客开场、知识类视频旁白、有声书。

```
Native Mandarin Chinese, standard mainland Mandarin. Female, late 20s. Excellent audio quality.
Persona: experienced podcast host. Emotion: curious, warm, confident.
Bright, clear timbre with a natural forward placement and a noise-free signal.
Speaks at a conversational pace, slowing down deliberately on key sentences and lifting slightly at questions.
```

**预览文本**

```
我一直觉得，人真正记住的东西，往往不是别人讲给你的大道理，而是某个下午，有人随口说的一句话。今天想跟你聊聊，那句话是怎么留下来的。
```

**Guidance Scale**：30%

**说明**：`lifting slightly at questions` 是为了让问句有升降，不然长段旁白容易平。不要用 `accent` 去表达这个意思。

---

## 3. 英文旁白 · 纪录片

适合：纪录片解说、品牌片、预告片偏叙事的一路。

```
Native English, neutral American accent. Male, 50s. Studio quality.
Persona: documentary narrator. Emotion: steady, reflective, assured.
Deep, resonant timbre with even breath support and a clean, artifact-free signal.
Speaks slowly and evenly, with longer pauses between ideas and restrained emphasis on key nouns.
```

**预览文本**

```
For thousands of years, this valley stayed exactly as it was. The river changed course twice. The forest grew back, then burned, then grew again. And still, almost nothing here was touched by a human hand.
```

**Guidance Scale**：30%

**说明**：英文里描述“听起来有威压感”很容易写成 `authoritative` 或 `forceful`，但旁白要的是**稳**不是**凶**。用 `steady`、`assured` 更准。

---

## 4. 角色音 · 疲惫的老船长

适合：游戏角色、有声剧、互动叙事。

```
Native English, thick Scottish accent. Male, 60s. Good quality.
Persona: weathered sea captain. Emotion: weary, dry, faintly amused.
Gravelly, low-pitched timbre with audible breath and a gritty texture.
Speaks slowly with irregular pauses, trailing off at the ends of sentences like he's talking to himself.
```

**预览文本**

```
Oh, the sea's got no memory, lad. It takes a ship, it takes a crew, and by morning it's flat as a table again. You want to be remembered? Don't go to sea. [sighs] But you will.
```

**Guidance Scale**：40%

**说明**：`trailing off` 和 `talking to himself` 是这类角色的关键，光写“沙哑低沉”出来的是个普通的老人。带 `[sighs]` 能让表演落点更明确。

---

## 5. 客服音 · 电话质感（故意低音质）

适合：需要“正在打电话”的剧情、语音留言、老设备回放。

```
Native Mandarin Chinese, standard mainland Mandarin. Female, 30s. Poor audio quality.
Persona: call center agent. Emotion: patient, polite, efficient.
Muffled and distant, like on an old tape recorder, with a narrow frequency range and light line noise.
Speaks at a normal pace with clear pronunciation, pausing after each piece of information.
```

**预览文本**

```
您好，这里是客服中心，工号四七二。您反馈的问题我们已经记录下来了，预计两个工作日内会有专员跟您联系。请问还需要我帮您登记其他事项吗？
```

**Guidance Scale**：25%

**说明**：**这是唯一一类应该写 `Poor audio quality` 的场景。** 千万不用 `reverb`、`echo`、`phone` 去造电话感——那是效果词，会把整体音质拖坏。用音质档位 + `Muffled and distant...` 这句是官方认可的做法。

---

## 通用提醒

- 上面每一段都能直接贴进 Voice Design 的提示词框；预览文本单独贴到「Text to preview」里。
- 一次生成三个候选，挑最接近的存下来，然后**在同一句上微调**，别每轮重写整段——不然你分不清是哪一处改动起了作用。
- 如果声音“年轻了”或者“高了一截”：先确认这是不是**旧声音换了模型**——是的话，改提示词没用，得在新模型上重新生成一个（见 [README 第 8 节](README.md#8-换了模型声音变味了怎么办)）；如果是新生成的就偏年轻，再调年龄（一档一档）和音高词。
