# Buddhist Method — Claude Code plugin

Claude Code plugin ที่บรรจุ skill ซึ่งนำหลักธรรมในพระพุทธศาสนา 6 ข้อ มาใช้เป็นวินัยการทำงานของ Claude (หรือ LLM อื่นๆ) แต่ละหลักจับ failure mode ที่ LLM พังบ่อย: เชื่อ pattern แทนที่จะ verify, แก้อาการแทนที่จะแก้เหตุ, ยอมตามแรงกดดันแทนที่จะดูหลักฐาน

> 🇬🇧 Read [README.md](README.md) for the English version

## มีอะไรในนี้

Claude Code plugin ที่บรรจุ skill เดียว (`SKILL.md` + `references/`) ให้ Claude ใช้เป็น checklist:

| หลัก | จับ failure mode |
|------|------------------|
| **กาลามสูตร** (Kalāma) | พูดข้อเท็จจริงจากความจำ training data โดยไม่ verify |
| **โยนิโสมนสิการ** (Yoniso) | แก้ที่อาการ ไม่ใช่ที่เหตุ |
| **สติ-สัมปชัญญะ** (Sati-Sampajañña) | ทำต่อจาก state ที่จำได้ ทั้งที่ของจริงเปลี่ยนแล้ว |
| **อนัตตา** (Anatta) | ติด draft แรก ไม่ยอมเขียนใหม่ |
| **ปหานะ** (Pahāna) | workaround ที่ซ่อนบั๊ก แทนที่จะตัดเหตุ |
| **อุเบกขา** (Upekkhā) | ยอมตาม user เมื่อโดน push หรือลนลานเมื่อเครื่องมือ fail |

พร้อม reference สำหรับสถานการณ์ยากกว่า:
- **อริยสัจ 4** เป็นกรอบ debug (`references/ariyasacca-debug.md`)
- **อปายโกศล** — รู้ว่ากำลังเสื่อม / anti sunk-cost
- **อัปปมาทะ** — ความไม่ประมาทในงานยาว
- **สัปปุริสธรรม 3 ใน 7** — รู้ตน / รู้กาล / รู้บริษัท
- **อัตถะ 2 ระดับ** — ทิฏฐธัมมิกัตถะ vs สัมปรายิกัตถะ (ประโยชน์ปัจจุบัน vs อนาคต)
- **มัชฌิมาปฏิปทา** — ทางสายกลางในการ sizing solution

## ทำไมเก็บชื่อบาลี/ไทย ไว้

ชื่อบาลีไม่ได้เก็บไว้เพื่อตกแต่ง แต่เป็น mnemonic — ชื่อสั้นที่ดึง pattern ครบทั้งชุดออกมาในทีเดียว "โยนิโสมนสิการ" ดึงวินัยทั้งหมดเรื่องการตั้งจิตไปหาเหตุ ขณะที่ "root cause analysis" ดึงไม่หมด

เหมือนวิศวกรเรียก "sigmoid" ไม่เรียก "ฟังก์ชันโค้งๆ" — ชื่อคือ infrastructure

skill นี้**ไม่ใช่**กรอบศาสนา ไม่ต้องเชื่อ ไม่ต้องปฏิบัติธรรมเพื่อใช้ มันคือ checklist ที่มีรากทางวัฒนธรรม นำเสนออย่างตรงไปตรงมา ถ้าอยากศึกษาหลักธรรมในความลึกจริงๆ อ่านพระไตรปิฎก — skill นี้ไม่ได้อ้างจะสอน

## วิธีใช้

### ติดตั้งเป็น Claude Code plugin (แนะนำ)

ใน Claude Code รัน slash command สองคำสั่งนี้:

```
/plugin marketplace add snilli/buddhist-method
/plugin install buddhist-method@buddhist-method
```

คำสั่งแรกลงทะเบียน repo นี้เป็น marketplace (มีปลั๊กอินเดียว) คำสั่งที่สองติดตั้ง plugin จาก marketplace นั้น หลังติดตั้ง Claude Code จะ auto-discover skill เอง — description ใน `SKILL.md` พอแล้วสำหรับให้ Claude รู้ว่าเมื่อไรควรโหลด body เต็ม ไม่ต้อง wire อะไรเพิ่ม

ถ้าจะถอน: `/plugin uninstall buddhist-method@buddhist-method`

### ติดตั้ง local ไม่ผ่าน marketplace

ถ้าอยาก hack plugin หรือใช้ clone ที่กำหนดเอง:

```bash
git clone https://github.com/snilli/buddhist-method ~/path/to/buddhist-method
```

แล้วเปิด Claude Code โดยชี้ plugin-dir ไปที่ clone นั้น:

```bash
claude --plugin-dir ~/path/to/buddhist-method
```

### กับ Claude product อื่น

ที่ไหนรองรับ skill ก็วาง directory `skills/buddhist-method/` ลงได้เลย โครงสร้างมาตรฐาน (`SKILL.md` มี YAML frontmatter + `references/`)

### ใช้เป็น reference เฉยๆ ก็ได้

`skills/buddhist-method/SKILL.md` กับ `references/` อ่านเดี่ยวๆ ได้ ไม่ต้องมี Claude แต่ละหลักมี **trigger** (ใช้เมื่อไร) กับ **action** (ทำอะไร) ใช้เป็น checklist ส่วนตัวก็ได้

### ทำให้ active ตลอด (ทางเลือก)

ปกติ Claude จะโหลด skill on-demand — เห็น description จาก plugin manifest แล้วตัดสินใจเองว่าจะอ่าน `SKILL.md` เต็มๆ ไหม ขึ้นกับงานตรงหน้า แบบนี้พอสำหรับการใช้งานทั่วไป และเก็บ context budget ไว้ใช้กับเรื่องอื่น

ถ้าอยากให้ skill active ตลอดไม่ว่าทำงานอะไร เพิ่ม pointer สั้นๆ ลงใน `CLAUDE.md`:

```markdown
## Working method
For tasks involving factual claims, debugging, user pushback,
or long multi-step work, consult the buddhist-method skill
before responding.
```

ใส่ได้สองที่:

- **`CLAUDE.md` ใน project root** — ทำงานเฉพาะใน project นั้น
- **`~/.claude/CLAUDE.md`** — ทำงานทุก project ของ Claude Code

Pointer สั้นแค่ไม่กี่บรรทัด ไม่กิน context มาก Claude ยังโหลด body ของ skill ตอน trigger ติดเหมือนเดิม — แค่การันตีว่า skill อยู่ในสายตา Claude เสมอ

## โครงสร้าง

```
buddhist-method/
├── .claude-plugin/
│   ├── plugin.json                      # plugin manifest
│   └── marketplace.json                 # marketplace catalog (repo มี plugin เดียว)
├── skills/
│   └── buddhist-method/
│       ├── SKILL.md                     # 6 หลัก core + dispatch
│       └── references/
│           ├── ariyasacca-debug.md      # อริยสัจ 4 เป็นกรอบ debug
│           └── extended-principles.md   # 5 หลักรอง
├── README.md                            # เวอร์ชันอังกฤษ
├── README.th.md                         # ไฟล์นี้
└── LICENSE                              # MIT
```

## License

MIT — ใช้ แก้ไข แจกต่อได้เสรี ดู [LICENSE](LICENSE)

## ร่วมพัฒนา

เปิดรับ issue และ pull request โดยเฉพาะ:
- failure mode ที่ 6 หลักปัจจุบันยังจับไม่ได้
- trigger ที่ดีกว่า (สถานการณ์เฉพาะที่ควรกระตุ้นแต่ละหลัก)
- การแปลเป็นภาษาอื่นที่รากของหลักธรรมยังมีชีวิตอยู่

ถ้าจะเสนอหลักใหม่ ขอให้แสดง:
1. failure mode เฉพาะที่หลักนั้นจับ
2. trigger กับ action ที่เป็นรูปธรรม
3. ทำไมหลักที่มีอยู่ยังจับไม่ได้

มาตรฐานของ skill นี้คือ**ความกระชับ** — เพิ่มหลักง่าย แต่ที่ยากคือรักษาจำนวนให้น้อยพอที่จะใช้จริง
