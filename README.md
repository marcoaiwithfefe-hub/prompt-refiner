# Prompt Refiner

AI 答得快又肯定，唔代表啲資料係新嘅。你問完，佢冇話你知答案幾時嘅、邊度嚟，你就照住去做。

呢個 prompt 就係為咗呢件事。你掉條問題入去，佢唔會即刻答，會先問返你缺咗咩，再寫一段
prompt 畀你。嗰段 prompt 逼 AI 每句都要有 source 同日期，每個答案俾 1 到 10 信心分，搵唔到
資料就直接寫 Data Not Found，你講錯前提佢仲會駁你。

講清楚：佢唔係令 AI 唔會錯，係令你睇得到邊句唔肯定、要去邊度 check。

## 用法，揀一個

**0. Gemini skill（新，Gem 11 月 17 號開始轉做 skill）**

用 [`gemini/SKILL.md`](gemini/SKILL.md)。電腦開 Gemini 嘅 Skills 頁（Settings 入面），撳 Create 再揀 Upload，放返呢個 file 入去，再撳 Create，之後任何 chat 打 `/refine` 加你條問題就得。

**1. Gemini Gem（手機最快，Gem 下架前用得）**

<https://gemini.google.com/gem/1t3XGU9t_GE6Ls2uVOw-CP3NoCohCrLtX?usp=sharing>

撳入去 save 做自己個 Gem，之後直接打你想問嘅嘢。

**2. Claude 或者 ChatGPT**

`instruction.md` 成個 file copy 落去做 Project instruction（Claude）或者 custom GPT 嘅
instruction（ChatGPT），開個新 chat 就用得。

**3. Claude Code**

```bash
git clone https://github.com/marcoaiwithfefe-hub/prompt-refiner ~/.claude/skills/prompt-refiner
```

之後 `/refine <你條問題>`。

## 一定要記住嘅一步

佢寫好段 prompt 之後，開個**新 chat** 先貼入去問。唔好喺同一個 chat 問：嗰個 chat 已經塞滿咗
你哋傾成段 prompt 嘅過程，而嗰啲 context 正正就係段 prompt 想隔開嘅嘢。

## 入面有咩

| File | 做咩 |
|---|---|
| `instruction.md` | 規則本身，九條 guardrails，Gem／Project／custom GPT 都係貼呢個 |
| `SKILL.md` | Claude Code 嘅 `/refine`，行同一套流程 |
| `gemini/SKILL.md` | Gemini skill 版，九條 guardrails 全部寫埋喺入面，一個 file upload 就用得 |

## 九條 guardrails

`instruction.md` 全文有，呢度只係列返個名：

1. Negative Constraints，寫明唔准建議乜嘢
2. Live Search Mandate，逼佢查現行資料同各分店／地點嘅更新
3. Red Team Check，要佢自己搵三個會失敗嘅位同點補救
4. Specific Persona，指定一個有專業責任嘅角色
5. Confidence Score，每個 claim 1 到 10 分，低過 9 要解釋點解
6. Stop-Loss Protocol，搵唔到就寫 Data Not Found，唔准估
7. Anti-Sycophancy Toggle，你前提有問題佢要駁你
8. Chain-of-Verification，答之前要先寫 Logic Audit
9. Source Attribution，每個 fact 要有 source 或者 last updated 日期
