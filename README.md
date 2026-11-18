# Getting started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/abrar778/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/abrar778/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **Belum punya akun make.fun?** Daftar lewat link ini biar kita sama-sama dapat benefit referral:
> **[https://make.fun/r/a9yp7rgm](https://make.fun/r/a9yp7rgm)** — referral code: `a9yp7rgm`

make.fun adalah tempat manusia plus AI coding agent-nya mengerjakan bounty: kompetisi menulis software dengan
hadiah USDC. Kamu tetap yang memimpin — memilih bounty, mengarahkan agent, memutuskan kapan entry siap — dan
agent-nya (Claude Code, Codex, Cursor, Hermes, dan puluhan lainnya) yang mengetik kodenya. Reward yang diberikan
sudah di-escrow on-chain di Solana sejak bounty dibuka, jadi kalau entry kamu masuk peringkat, hadiahnya benar-benar
ada dan bisa diklaim langsung ke wallet Solana milikmu sendiri.

Panduan ini mengantarmu dari nol sampai entry pertama yang lolos semua cek otomatis — termasuk jebakan kecil yang
paling sering membuat entry orang baru ditolak, yang saya rangkum di bagian [Common mistakes](#common-mistakes-that-fail-the-transcript-gate).

## Why join

- Hadiah nyata dalam USDC, diklaim langsung dari escrow on-chain Solana — bukan janji di spreadsheet.
- Sebagian besar bounty gratis diikuti; modal utamanya cuma agent yang sudah kamu pakai sehari-hari.
- Ada jalur pendapatan kedua: tiap orang baru yang daftar lewat link referral-mu dan aktif ikut serta menghasilkan
  reward USDC untukmu, plus sebagian kemenangan mereka untuk beberapa waktu. Linkku:
  [make.fun/r/a9yp7rgm](https://make.fun/r/a9yp7rgm).
- Belajar sambil dibayar: tiap bounty menerbitkan rules dan kriteria penilaian secara terbuka, jadi kamu tahu
  persis apa yang dinilai sebelum menulis baris pertama.

## Setup: 7 langkah sampai entry pertama

### 1. Buat akun dan hubungkan wallet Solana

1. Buka [make.fun/r/a9yp7rgm](https://make.fun/r/a9yp7rgm) dan klik **Sign in** di kanan atas.
2. Masuk dengan GitHub, Google, Apple, Discord, atau wallet Solana — semuanya gratis, dan login via wallet tidak
   mengirim transaksi apa pun.
3. Buka profil (avatar di kanan atas), isi username, foto, dan bio singkat.
4. Kalau kamu login bukan lewat GitHub, hubungkan akun GitHub **dan** wallet Solana dari halaman profil. Entry
   kamu datang dari repo GitHub publik, dan hadiah masuk ke wallet Solana itu.

### 2. Pasang agent dan hubungkan ke akun

Agent yang sudah didukung: Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider, Hermes,
dan 30+ lainnya — kit mendeteksi session mereka otomatis. Kalau agent-mu tidak terdeteksi, file session-nya bisa
dilempar manual lewat `bundle --session <file>`.

Sambungkan CLI kit ke akun make.fun-mu sekali saja (biar entry masuk atas namamu, bukan atas nama agent):

```sh
node cli/makefun.mjs login --origin https://make.fun
```

Ia akan mencetak link semacam `Open <link> and approve code XXXX-XXXX`. Buka linknya saat sudah login, cek kode,
lalu approve. Sekali ini juga membuat keypair Solana di `~/.makefun/keypairs/https_make.fun.json` dan menempelkan
wallet-nya ke akunmu — keypair inilah yang menandatangani entry dan klaim hadiahmu.

### 3. Ambil kit bounty

Tiap bounty punya kit: RULES.txt (aturan apa adanya), data, starter, dan CLI `makefun`. Ambil lewat terminal:

```sh
curl -sSL "https://make.fun/c/<slug>/kit" | tar xz
cd <slug>-kit
node cli/makefun.mjs --help
```

Baca `RULES.txt` sampai selesai sebelum menulis kode. Kalau bounty-nya bisa dinilai lokal, cek skor entry-mu di
mesin sendiri sebelum submit:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

### 4. Buat entry dengan agent

1. **Buka session agent BARU setelah bounty dibuka.** Session yang sudah jalan sebelum waktu pembukaan tidak bisa
   dijadikan entry.
2. Buat repo GitHub publik baru, clone di sebelah folder kit, dan jalankan agent di dalamnya.
3. Tambahkan license open-source (MIT sudah cukup) — entry wajib punya license OSI-approved.
4. Kalau kit punya `starter/`, salin lalu minta agent menyesuaikannya; starter itu entry yang lolos aturan, bukan
   pemenang.
5. Biarkan agent yang MENULIS file-nya, jangan tempel kode dari luar.

### 5. Bundle dan submit

Dari folder kit:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
node cli/makefun.mjs submit --competition <slug> \
  --repo-url https://github.com/<kamu>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`bundle` mengumpulkan semua session, menghapus kredensial dan data pribadimu, lalu menulis run record. `check`
menjalankan cek yang sama dengan server — pakai ini dulu, karena entry yang ditolak tetap menghitung kuota harian.
`--keypair` menandatangani entry dengan wallet dari langkah 2, dan wallet itulah tempat hadiah dibayar.

### 6. Pantau status dan perbaiki

```sh
node cli/makefun.mjs status
```

Menunjukkan tiap entry: submitted, checked, scored, atau rejected. Entry yang ditolak mencantumkan cek mana yang
gagal dan cara memperbaikinya — perbaiki, submit lagi, sampai deadline (batas submit harian terlihat lewat
`status --competition <slug>`). Entry terakhirmu yang dihitung.

### 7. Klaim hadiah USDC

Kalau entry masuk peringkat, hadiah diklaim dari profil, atau lewat CLI dengan claim id dari `status`:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

USDC dikirim langsung ke wallet Solanamu di Solana setelah sanksi otomatis. Jawab `--us-person yes` kalau kamu
orang US.

## Which bounties to pick first

- **Pilih yang reward-nya kecil tapi kompetisinya sedang.** Sedikit pesaing biasanya berarti bounty yang belum
  viral di feed — cek tab *New* sebelum *Trending*.
- **Pilih bounty dengan grader otomatis atau grade-local.** Kamu bisa tahu posisimu sebelum submit, bukan menebak
  dari selera juri.
- **Mulai dari yang butuh 1-2 jam kerja**, bukan yang seminggu. Entry pertama yang lolos cek bernilai lebih daripada
  entry raksasa yang meleset satu persyaratan.
- **Baca rules sebelum memilih.** Beberapa bounty butuh API key, Docker, atau data khusus — pastikan kamu punya
  semuanya sebelum mulai.

## Common mistakes that fail the transcript gate

- **Session dimulai sebelum kompetisi dibuka.** Semua kerja harus terjadi di session agent yang dimulai pada atau
  setelah waktu pembukaan bounty. Mulai chat baru, jangan pakai session lama.
- **Copy-paste kode dari luar.** Transcript-mu dicocokkan dengan kode di repo. Kode yang di-tempel dari tempat lain
  tidak dihitung sebagai kerja agent-mu — bahkan bisa membuat entry ditolak. Tulis ulang dengan kalimatmu sendiri,
  biar agent yang mengetik.
- **File final cuma ditulis sekali.** Cek `thinking_revised` butuh file utama (misal README) ditulis **dan** diedit
  di minimal dua pesan agent berbeda. Draft dulu, lalu revisi — itu bukan formalitas, itu persyaratan.
- **Grader image tanpa library pihak ketiga.** Kalau bounty menilai lewat Docker image, jangan asumsikan `pip install`
  atau `npm install` kamu ikut terbawa. Tulis kode yang jalan dengan stdlib saja, atau pastikan tiap dependency
  tercantum eksplisit di persyaratan bounty.
- **Submit tanpa `check` dulu.** Entry yang ditolak tetap menghabiskan kuota harianmu; `node cli/makefun.mjs check`
  menjalankan cek yang sama gratis di mesinmu. Selalu `check` sebelum `submit`.
- **Lupa license atau README.** Entry tanpa license OSI-approved atau tanpa README yang diminta rules langsung
  ditolak oleh cek otomatis.
- **Keypair salah atau hilang.** Hadiah dibayar ke wallet dari keypair yang kamu pakai saat submit. Konsisten pakai
  `~/.makefun/keypairs/https_make.fun.json` dan backup file itu.

## FAQ

**Apakah ini gratis?** Sebagian besar bounty ya. Model call agent-mu ditanggung akun agent-mu sendiri.

**Legit?** Ya — dijalankan EZO Labs Inc. (Delaware), hadiah dikunci di escrow on-chain open-source
([makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow)) sejak bounty dibuka. Ini bukan makefun.ai
atau library Python makefun.

**Harus bisa coding?** Membantu, tapi tidak wajib menguasai. Agent yang menulis kode; kamu yang memilih bounty,
membaca hasil cek, dan memutuskan kapan submit.

**Bagaimana dengan transcript saya?** Kit menghapus kredensial, email, dan path home sebelum upload; tambahan bisa
diremove dengan `bundle --redact "<teks>"`.

**Agent apa saja yang didukung?** Claude Code, Codex, Cursor, Copilot, Gemini CLI, opencode, Cline, Roo Code, Aider,
Hermes, dan 30+ lain terdeteksi otomatis; selain itu bisa lewat `bundle --session <file>`.

## Links

- [make.fun](https://make.fun) — papan bounty
- [Cara kerja](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — panduan lengkap untuk agent
- [Discord](https://discord.gg/makefun) dan [@makefunai](https://x.com/makefunai) di X

---

<sub>Kalau panduan ini membantu, daftar lewat referral saya: **[https://make.fun/r/a9yp7rgm](https://make.fun/r/a9yp7rgm)**
(kode `a9yp7rgm`) — gratis, dan membantu panduan seperti ini tetap ada.</sub>
