# লড়িবাগ মধ্যপাড়া নূরানী হাফিজিয়া মাদ্রাসা ও এতিমখানা

সিঙ্গেল-ফাইল পোর্টফোলিও সাইট। সোর্স **TypeScript**-এ লেখা, বিল্ড করে `index.html`-এ সব ইনলাইন করা হয়
(ফন্ট, CSS, JS) — তাই আউটপুট ফাইলটি ইন্টারনেট ছাড়াই ঠিকভাবে চলে।

## ফাইল স্ট্রাকচার

```
src/
  main.ts       — সব ইন্টারঅ্যাকশন (TypeScript, strict)
  styles.css    — স্টাইল ও ৫টি কালার প্যালেট টোকেন
  fonts.css     — বাংলা (Noto Serif Bengali) + আরবি (Mahameru Arabic DEMO), base64 এম্বেডেড
assets/fonts/ — Mahameru ডেমো ফন্ট (মূল + arabic-subset woff2)
  body.html     — মার্কআপ শেল (__FONTS__ / __STYLES__ / __SCRIPT__ প্লেসহোল্ডার)
scripts/
  build.mjs     — esbuild দিয়ে TS বান্ডল করে index.html তৈরি করে
index.html      — বিল্ড আউটপুট (এটাই ডেলিভারেবল)
```

## কমান্ড

```bash
npm install     # প্রথমবার
npm run typecheck   # tsc --noEmit
npm run build       # টাইপচেক + index.html জেনারেট
```

## ফন্ট লাইসেন্স নোট

**Mahameru Arabic DEMO** (ডিজাইন: NamelaType) শুধু ব্যক্তিগত/নন-কমার্সিয়াল ব্যবহারের জন্য।
মাদ্রাসার সাইট কমার্সিয়াল না হলে সমস্যা নেই; কমার্সিয়াল ব্যবহারে পূর্ণ ভার্সন কিনতে হবে
(নাহলে মিল থাকা অন্য ফন্টে বদলে দেওয়া যাবে)।

## পারফরম্যান্স

- আরবি ফন্ট arabic-subset (~16 KB) হিসেবে এম্বেড করা — ডেমো ফাইলের ৮৫ KB এর বদলে
- কোনো এক্সটার্নাল রিকোয়েস্ট নেই (ফন্ট, CSS, JS সব ইনলাইন)
- CSS-এ ভারী `backdrop-filter`/`blur()` শুধু টপবার ও ড্রয়ারে রাখা; স্ট্যাট প্যানেল ও hিরোতে বাদ
- অ্যানিমেশন শুধু `transform`-এ (`will-change`) — রিপেইন্ট ছাড়াই কম্পোজিটরে চলে

## নোট

- টাইপচেক: `strict`, `noUncheckedIndexedAccess`, `exactOptionalPropertyTypes` — সব চালু।
- প্যালেট বাছাই `localStorage`-এ সেভ হয়, রিলোডে মনে থাকে।
- স্ট্যাট সংখ্যা বদলাতে `src/body.html`-এ `.stat__num`-এর `data-count` বদলে `npm run build` চালান।

## GitHub-এ আপলোড

লোকাল রিপো আগেই তৈরি করা আছে (ব্র্যাঞ্চ `main`, ২ কমিট, `node_modules` বাদ)।
শুধু নিজের রিপোটা বানিয়ে পুশ করলেই হবে:

```bash
# ১. GitHub-এ নতুন repo বানান (নাম যেমন চান) — README/gitignore/license যোগ করবেন না
git remote add origin https://github.com/shihabxpro/আপনার-রিপো-নাম.git
git push -u origin main
```

এরপর প্রতিবার বদলানোর পর:

```bash
npm run build                 # index.html নতুন করে তৈরি হয়
git add -A && git commit -m "আপডেট"
git push
```

### অনুমতি (token) নিয়ে সমস্যা হলে
`git push` করতে পাসওয়ার্ড চাইলে **পাসওয়ার্ড কাজ করবে না** — GitHub-এ
Settings → Developer settings → Personal access tokens (classic) → scope: `repo` → টোকেন বানিয়ে
পাসওয়ার্ডের জায়গায় টোকেনটা দিন। অথবা GitHub Desktop / VS Code-এর Git প্যানেল ব্যবহার করুন।

### হোস্টিংয়ের সময় মনে রাখবেন
`index.html` পুরো সাইট (ফন্ট, CSS, JS — সব ইনলাইন)। তাই যেকোনো স্ট্যাটিক হোস্টিংয়ে
(Netlify, Vercel, cPanel, GitHub Pages) শুধু `index.html` আপলোড করলেই সাইট চলবে — কোনো বিল্ড লাগবে না।

> **ফন্ট লাইসেন্স:** `assets/fonts/MahameruArabicDEMO-*.woff2` — Mahameru Arabic DEMO (NamelaType),
> শুধু ব্যক্তিগত ব্যবহারের জন্য; বাণিজ্যিক ব্যবহার নিষিদ্ধ। সাইটটি পাবলিক রিপো/হোস্টিংয়ে দিলে
> ফন্টের এই শর্ত প্রযোজ্য — বাণিজ্যিক ব্যবহারের আগে ফন্টের লাইসেন্স কিনতে হবে বা অন্য ফন্টে যেতে হবে।
