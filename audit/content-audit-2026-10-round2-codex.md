# Content Audit Round 2 — Codex (gpt-6.1-sol) · 2026-10-02

Run: `~/.hermes/codex-runs/20261002T102103Z_AEvy25/` (498s, ~100k tokens, exit 0)
โจทย์: ตรวจการแก้รอบ 1 + หา finding ใหม่ · ผลรวม: แก้ครบทั้ง A และ B ใน commit ถัดจากไฟล์นี้

## A) ตรวจการแก้รอบ 1 — YES 8 / PARTIAL 4 / NO 0

PARTIAL 4 จุด → เก็บตกครบแล้วใน commit นี้:
- #2 DORA: ยังมีคำว่า "DORA 4" ค้างในกล่องท่องจำท้ายหน้า → เปลี่ยนเป็น "DORA 5 metrics"
- #7 git reset --hard: "untracked ไม่หาย" เด็ดขาดเกิน (ไฟล์ที่ขวางทางอาจถูกลบ) → แก้ถ้อยคำ
- #8 leftmost prefix: ต้อง harmonize ทั้งไฟล์ (เนื้อหาหลัก + self-check + flashcard) → แก้ครบ 3 จุด
- #9 causal mask: self-check Q1 ยังพูดกว้าง ("ทุก token") → แก้เป็น "ตำแหน่งที่มองเห็น — ปัจจุบันและก่อนหน้า"

## B) Findings ใหม่ 25 ข้อ (CRITICAL 0 · MODERATE 20 · MINOR 5) → triage + แก้ครบ

| # | Sev | เรื่อง | การแก้ |
|---|-----|-------|--------|
| 1 | MOD | `.claudeignore`/`.gitignore` ไม่ใช่ access control | แก้เป็น permission/deny rules + โน้ต .gitignore กันแค่ commit |
| 2 | MOD | BCNF = superkey (ไม่ใช่ candidate key) + 3NF นิยามเข้ม | แก้ sheet + flashcard |
| 3 | MOD | `git restore` default source = index (ไม่ใช่ commit) | แก้ตาราง + ระบุ --source=HEAD |
| 4 | MOD | quicksort in-place ยังมี recursion stack O(log n)/O(n) | แก้ 3 จุด + flashcard |
| 5 | MOD | FK อ้าง UNIQUE key / ตารางตัวเองได้ | แก้ |
| 6 | MOD | parameterized query ใช้กับ identifier/SORT ไม่ได้ → allowlist | แก้ + ตัดคำ "เท่านั้น" |
| 7 | MOD | 403 ไม่ได้การันตีว่า authenticate แล้ว (RFC 9110) | แก้ |
| 8 | MOD | immutable ≠ hashable (tuple มี list = ใช้เป็น key ไม่ได้) | แก้การ์ด |
| 9 | MOD | default bridge: container คุยกันด้วย IP ได้, -p ไว้เปิดรับนอก | แก้ |
| 10 | MOD | rolling "ไม่ downtime" เด็ดขาดเกิน | แก้ sheet + flashcard (มีเงื่อนไข readiness) |
| 11 | MOD | exec form ไม่ได้ reap child ให้เอง → แอปต้องทำ/ใช้ --init | แก้ sheet + flashcard |
| 12 | MOD | Sprint Backlog = Sprint Goal + งานที่เลือก + แผนส่งมอบ | แก้ |
| 13 | MOD | Sprint Review = working session (ไม่ใช่แค่ presentation) | แก้ sheet + flashcard |
| 14 | MOD | E2E ไม่จำเป็นต้องผ่าน UI (API ก็ได้) | แก้ |
| 15 | MOD | **DORA 2024: AI → delivery throughput ลดลง** (เดิมเขียน "เพิ่ม") | แก้ — จุดสำคัญสุดของรอบนี้ |
| 16 | MOD | โมเดลมี parametric knowledge จริง (ไม่ใช่ "ไม่รู้ข้อเท็จจริง") | ปรับถ้อยคำ 3 จุด + flashcard |
| 17 | MOD | RAG ไม่จำเป็นต้องใช้ embedding/vector DB (lexical ได้) | แก้ |
| 18 | MOD | quantization: memory ลดเป็นหลัก, speed มีเงื่อนไข hardware | แก้ sheet + flashcard |
| 19 | MOD | memory ไม่ได้ inject ทุกครั้งเสมอ (อ่าน on demand ได้) | แก้ตาราง + flashcard |
| 20 | MOD | hybrid search ไม่ชนะทุกกรณี — ต้อง eval | แก้ |
| 21 | MIN | float == : ใช้ tolerance (ไม่ใช่ห้ามเด็ดขาด) | แก้ 2 จุด |
| 22 | MIN | Sprint ≤ 1 เดือน มีตั้งแต่ Guide 2017 ไม่ใช่ 2020 | ตัดข้ออ้างปี |
| 23 | MIN | Node 20 EOL (เม.ย. 2026) → ตัวอย่างเปลี่ยนเป็น Node 24 | แก้ Dockerfile ตัวอย่าง |
| 24 | MIN | PATCH = bugfix แบบ backward-compatible | แก้ sheet + flashcard |
| 25 | MIN | ข้ออ้าง spacing D+1/D+7/D+21 ตรงเป๊ะทุกหัวข้อไม่จริงตามตาราง | reframe เป็น "เป้าหมาย" + buffer days |

## Notes
- ทุก finding ถูก verify กับแหล่งจริงก่อนแก้ (RFC 9110/9700, dora.dev, scrumguides.org, semver.org, git-scm, docs.docker.com, Python docs) — ไม่แก้ตาม report เชื่อๆ
- รอบ 1 และ 2 ครบแล้ว: รวมแก้ทั้งหมด 37 จุด (12 + 25)
