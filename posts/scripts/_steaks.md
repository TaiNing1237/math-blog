# The $2,000 Math Problem I Solved (But Got Paid $0)

## Part 1: The Story 

老話說得好：『主動找上門的生意，通常不是好生意。』我以為我已經學乖了，但這次... 我還是沒學乖。

幾週前，矽谷著名的 AI 公司 Mercor 主動發信給我，邀請我為他們的 AI 模型出數學題。 合約看起來很誘人：時薪 50 ~ 90 美金。如果通過審核，還有額外的 Signing Bonus。

當時我已經一陣子沒收入了，心想：這不就是為我準備的嗎？ 我想起了以前看過的一個幾何移動問題，但我不會證明。 我花了整整兩天，進入了完全的心流狀態，想破了頭，終於證明出來了。

後來我去查資料，才發現這其實是 2018 年 IMO Shortlist 的 C3 難題。 說實話，還好我當時沒去查。如果知道是 IMO C3，而且他只要求證明一個比較弱的結論，我應該早就放棄了。 正因為不知道，我誤打誤撞，給出了一個比 IMO 解答更強的結果。我蠻相信這是一個新的發現。

我當時覺得：這是我今年最得意的作品，這 2000 美金拿定了。

結果呢？ 提交三天，審核中。 提交五天... 合約整個被單方面解除。不要說 2000 美金，我連其他好幾題還在審核中的費用都沒拿到。理由？沒有理由。沒有審核通過，當然，也就沒有錢。

根據合約，既然他們沒付錢，這題的 Intellectual Property (IP) 就還屬於我。 所以我想，與其讓這道漂亮的證明躺在我的硬碟裡發霉，不如把它免費獻給 YouTube 的觀眾。

沒錯，今天我要教你們這道『價值 2000 美金』的題目。 他們沒眼光買單，那是他們的損失。 現在，我們來看看這題數學，到底有多美。」

## Part 2: The Meat (The Mathematics)

### 1. The Setup: The Steak Tower

Let's dive into the core of the problem. Imagine a table with 1,025 plates. On the leftmost plate, Plate 0, we have a tower of 1,024 steaks. The goal is simple: move all of them to the last plate on the right. But we have a very specific physical constraint.

You can only move the top steak of any stack. And the distance it can travel depends on the current height of the stack it’s leaving. If a plate has $k$ steaks, the top one can jump to any plate within a distance of $k$. In short: The taller the tower, the longer the range.

Let’s start small. One steak, distance 1? Easy. Height is 1, jump 1. One step.

What about two steaks, distance 2? You can't just jump the bottom steak because it’s pinned down. If you jump the top steak (Steak A) all the way to Plate 2, Steak B is left alone at Plate 0. Now the height is 1, so Steak B can only jump to Plate 1. You'll need an extra move to get it to Plate 2, totaling 3 steps. This is the fundamental friction of the game.

### 2. The IMO Connection: The Stones vs. The Steaks

Math nerds might recognize this. It’s a variant of the IMO 2018 Shortlist Problem C3, where they moved stones. But when I was designing this for Mercor, I changed them to steaks—partly because they stack better, and partly because I wanted to push the difficulty.

In the IMO version, you only need to prove a loose lower bound: $\sum_{i=1}^{n} \lceil n/i \rceil$. The proof is elegant—you label the steaks and show that Steak 1 always needs $n$ steps, Steak 2 needs at least $n/2$, and so on. But that’s just an estimate. It doesn't show you how to achieve it. In fact, that bound is only tight for $n = 1, 2, 3, 4, 5, 7$. For everything else, the real answer is much higher. We need a tighter tool.

### 3. Finding the Pattern: Divide and Conquer

Let’s try a different philosophy: Divide and Conquer. Suppose $F(n)$ is the minimum steps to move $n$ steaks across distance $n$. What if we set up a checkpoint at Plate $k$?

Here’s the plan: We launch one steak directly to the finish line—Plate $n$—leveraging the full height. Then, we fly $(n-k-1)$ steaks directly to Plate $k$. Then we use $F(k)$ steps to move the remaining $k$ steaks to Plate $k$. Now the whole team (except one) is at the checkpoint. Then we fly $(k-1)$ steaks from the top of the tower at $k$ to $n$. Finally, we move the remaining $(n-k)$ steaks to the end using $F(n-k)$ steps.

The total cost? $(n-k-1) + F(k) + 1 + (k-1) + F(n-k)$. It simplifies beautifully to:
$$F(n) = (n-1) + F(k) + F(n-k)$$
But is this actually optimal? It feels intuitive, but in math, intuition is a dangerous substitute for proof. What if a steak 'skips' the checkpoint? What if some steaks 'start early' and don't wait at Plate $k$? If the recursive structure breaks, this whole formula collapses.

### 4. The Breakthrough: The "Surgery" Proof

This is where I was stuck for the longest time. I tried to find a decreasing invariant, but nothing worked. Then, I found the 'Surgery'—a way to strictly prove that this recursive structure is never worse than any other possible strategy.

Think about any arbitrary, chaotic set of moves. We find the smallest index $k^*$ from which any steak jumps directly to the finish line $n$. If we have moves that 'jump over' this $k^*$—say, from $i \to j \to p$ where $i < k^* < j$—we perform surgery.

We replace $\{(i, j), (j, p)\}$ with $\{(i, k^*), (k^*, p)\}$. We can prove this is always legal. $i \to k^*$ is a shorter jump, and $k^*$ is guaranteed to have the capacity because it's a launchpad for the finish line. By repeating this surgery, we eliminate all moves that bypass our checkpoint. We’ve effectively reduced any 'wild' strategy into a structured, recursive one without adding a single step.

This reduction is the key. It proves that the minimal cost must satisfy our recursive formula. All we have to do now is solve it.


## Part 3: The ending

雖然 Mercor 沒有付錢給我，但我還是很高興能把這個漂亮的數學題目分享給大家。希望你們喜歡這道題目的美麗證明，並且從中獲得啟發。



