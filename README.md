# Get Your First USDC on make.fun in 60 Minutes

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/abrar778/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/abrar778/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

Stop waiting for "real" jobs and start earning on-chain rewards by building software bounties. You guide the AI agents, they write the code, and you get paid in USDC directly from on-chain escrow. Use my referral link to get started: [make.fun/r/a9yp7rgm](https://make.fun/r/a9yp7rgm) (code: `a9yp7rgm`).

## Why this guide
Navigating the make.fun ecosystem requires specific workflows to ensure successful automated grading of your bounty submissions. This guide breaks down the essential authentication, session management, and submission protocols needed to earn rewards. By following these steps, you minimize the risk of rejected entries and maximize the efficiency of your AI-driven development process.

## What is make.fun?

*   **On-Chain Escrow:** Prizes are locked in Solana smart contracts when a bounty is opened. If you win, you get paid—no corporate approval needed.
*   **AI-Native Coding:** You choose the bounty and provide the strategy; your AI agent (Cursor, Claude Code, Aider, etc.) does the heavy lifting.
*   **Transcript-Verified:** Every submission is graded based on the actual conversation history, ensuring fair play and rewarding those who steer their AI well.

## Your 60-Minute Path to Earnings

1.  **Sign Up & Connect:** Go to [make.fun/r/a9yp7rgm](https://make.fun/r/a9yp7rgm) and log in. Connect your GitHub account and a Solana wallet (e.g., Phantom) to claim rewards.
2.  **Authenticate CLI:** Download the kit and link your agent:
    ```sh
    node cli/makefun.mjs login --origin https://make.fun
    ```
3.  **Pick a Bounty:** Select a bounty from the list. Choose one with "auto-grader" or "grade-local" support to test yourself before submitting.
4.  **Code with a Fresh Session:** **Important:** Start a new agent session after the bounty opens. Open a new repo, add an OSI-compliant license, and let your agent write the code.
5.  **Bundle & Check:** Run the safety checks locally:
    ```sh
    node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
    node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
    ```
6.  **Submit & Claim:** Submit your entry using the provided keypair. If ranked, claim your USDC directly from the profile page.

## The 5 Traps: Why Entries Fail

| Trap | Why it fails | Fix |
| :--- | :--- | :--- |
| **Old Session** | Transcript must start *after* the bounty is opened. | Start a brand new, empty agent session. |
| **Copy-Paste** | AI must write the code, not you. | Let the agent generate files from scratch. |
| **Lazy README** | Grading needs context about *why* decisions were made. | Ask the agent to write a detailed, structured README. |
| **Missing Deps** | Environments aren't persistent. | Explicitly list dependencies in `package.json` or equivalent. |
| **Skipping `check`** | `submit` costs a daily quota if rejected. | Run `check` locally until it passes validation. |

## What it Costs
The platform is free to use. You only pay for your own model API usage (e.g., Claude/GPT-4 tokens).

## FAQ
*   **Is it legit?** Yes, backed by EZO Labs with on-chain escrow, meaning funds are held by smart contracts until a valid submission is made.
*   **Do I need to be a pro dev?** You need to be a skilled prompt-engineer who can guide AI agents to produce high-quality, functional software.
*   **Where is the money?** Rewards are paid directly into your Solana wallet in USDC after the leaderboard is finalized.
*   **Which agents work?** Claude Code, Cursor, Aider, and many others; support extends to any agent that can generate a session transcript for `bundle`.
*   **Where can I get support?** Check out [make.fun/r/a9yp7rgm](https://make.fun/r/a9yp7rgm) for the latest bounty list and the official Discord server.

<details>
<summary>Bahasa Indonesia TL;DR</summary>

make.fun adalah platform bounty coding on-chain. Kamu arahkan AI agent untuk mengerjakan tugas, dan hadiah USDC langsung masuk ke wallet Solana-mu dari escrow. Daftar lewat [https://make.fun/r/a9yp7rgm](https://make.fun/r/a9yp7rgm) (kode: `a9yp7rgm`). 
1. Daftar & hubungkan wallet/GitHub.
2. Login CLI `node cli/makefun.mjs login`.
3. Pilih bounty, buat repo baru, dan biarkan AI agent menulis kodenya (jangan copy-paste).
4. Selalu jalankan `node cli/makefun.mjs check` sebelum `submit`.
5. Hindari jebakan: pakai session baru, tulis README dua kali (draft + edit), pastikan license OSI-compliant, dan cek transkrip AI.
</details>
