# 情境 01 — git stash：工作做到一半，任務來了

## 🎬 情境描述

### 前置步驟：讓 branch 產生差異

> **為什麼需要這個步驟？**  
> Git 切換 branch 時，只有在「切過去會蓋掉你目前的修改」時才會擋住你。  
> 因為 `feature-your-name` 是從 `main` 開出來的，兩個 branch 的 `index.html` 內容完全一樣，  
> 所以就算你修改了但沒 commit，Git 切過去也不會有衝突，就直接讓你切了。  
> 我們需要先在 `feature-your-name` 上 commit 一個修改，讓它跟 `main` 不同，  
> 之後再修改同一個地方，Git 才會真的擋住你。

確認你在 `feature-your-name` branch 上，先在 `src/index.html` 加入以下內容並 commit：

```html
<section class="hero">
  <p>這是一個用來練習 Git 指令的示範頁面。</p>
  <p>版本：v1.0</p>
</section>
```

```bash
git add src/index.html
git commit -m "feat: add version label to hero section"
```

---

### 正式情境開始

現在繼續修改 `src/index.html`，把版本號改成 `v2.0`，但**先不要 commit**：

```html
<p>版本：v2.0</p>
```

這時候，協作者說：

> 「等一下，`main` 上有個小 bug 需要你先去修，  
>  你能切過去看一下嗎？」

你輸入：

```bash
git checkout main
```

然後看到這個錯誤：

```
error: Your local changes to the following files would be overwritten by checkout:
        src/index.html
Please commit your changes or stash them before you switch branches.
```

😅 Git 不讓你切換——因為你有未提交的變更。

---

## 🎯 你的任務

在**不 commit** 目前修改的前提下，切換到 `main` branch。

---

## 💡 提示

<details>
<summary>想一下再看</summary>

有一個指令可以把目前的工作進度「暫時收起來」，  
讓你的工作區變乾淨，之後再拿回來。

</details>

<details>
<summary>指令提示</summary>

```bash
git stash
git checkout main
```

</details>

---

## ✅ 完成條件

1. 成功切換到 `main` branch。
2. 回到 `feature-your-name`，用以下指令把進度拿回來：

```bash
git checkout feature-your-name
git stash pop
```

3. 確認 `src/index.html` 的修改還在。

---

## 🧠 觀念筆記

| 指令 | 說明 |
|---|---|
| `git stash` | 把目前未 commit 的變更暫時存起來，工作區恢復乾淨 |
| `git stash pop` | 把最近一次 stash 的內容還原回工作區 |
| `git stash list` | 查看目前有哪些 stash 存著 |

> **什麼時候用 stash？**  
> 工作做到一半，需要臨時切換 branch，但又不想為了切換而製造一個「半成品 commit」時。

---

## ➡️ 完成後

前往 [情境 02 — git reset](./02-reset.md)