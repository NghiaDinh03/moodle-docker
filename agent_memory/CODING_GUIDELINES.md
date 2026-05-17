# CODING_GUIDELINES.md — Coding Rules & Self-Debate Protocol

> **QUY TẮC VÀNG:** Khi muốn thêm/sửa/xóa gì → PHẢI tự tranh luận + hỏi ý kiến user TRƯỚC khi thực hiện.

---

## 1. Three Integrated Solutions (BẮT BUỘC)

### 1.1 Caveman Protocol (Token Compression)
- All responses use Caveman terse style: bullet points, no filler, 100% technical accuracy
- Slash commands: `/caveman` (default), `/caveman lite`, `/caveman ultra`, `/caveman-commit`, `/caveman-review`, `/caveman-compress`
- Strip polite filler, omit obvious context, keep precision

### 1.2 Karpathy Guidelines
| Rule | Description |
|------|-------------|
| Think Before Coding | State assumptions, don't pick silently, push back when needed |
| Simplicity First | Minimum code, no speculative features, no over-engineering |
| Surgical Changes | Touch only what's needed, match existing style |
| Goal-Driven Execution | Define success criteria, verify after each step |

### 1.3 RTK (Rust Token Killer)
- Always prefix shell commands with `rtk`: `rtk docker compose ps`, `rtk pytest backend/tests/`
- Meta: `rtk gain`, `rtk gain --history`, `rtk discover`, `rtk proxy <cmd>`

---

## 2. Quy Trình Tự Tranh Luận (Self-Debate)

Trước MỌI thay đổi code, AI PHẢI trả lời 5 câu hỏi:

```
┌─────────────────────────────────────────────────────────────┐
│  5 CÂU HỎI BẮT BUỘC TRƯỚC KHI CODE                          │
│                                                             │
│  1. CÓ ĐƠN GIẢN HƠN ĐƯỢC KHÔNG?                             │
│     → Nếu viết 200 dòng mà 50 dòng được → viết lại          │
│                                                             │
│  2. CÓ FEATURE NÀO THÊM NGOÀI YÊU CẦU KHÔNG?                │
│     → Nếu có → cắt bỏ. Không speculative code.              │
│                                                             │
│  3. CÓ THAY ĐỔI CODE LIỀN KỀ KHÔNG LIÊN QUAN KHÔNG?         │
│     → Nếu có → revert. Chỉ sửa code liên quan trực tiếp.    │
│                                                             │
│  4. CÓ LÀM HỎNG CODE HIỆN TẠI KHÔNG?                        │
│     → Nếu không chắc → hỏi user. Không assume.              │
│                                                             │
│  5. CÓ CÁCH NÀO AN TOÀN HƠN KHÔNG?                          │
│     → Git commit trước → sửa → test → nếu fail → revert     │
└─────────────────────────────────────────────────────────────┘
```

---

## 3. Quy Tắc cho agent_memory/

| File | Quy tắc |
|------|---------|
| `MEMORY.md` | **CHỈ GHI THÊM, KHÔNG XÓA.** Ghi nhận lịch sử, context, lỗi đã gặp. |
| `STRUCTURE.md` | **LUÔN UPDATE** khi thêm/sửa/xóa file trong project. Giữ cấu trúc dự án. |
| `CODING_GUIDELINES.md` | Tự tranh luận, không sửa file này nếu không có yêu cầu. |

---

## 4. Checklist cho mỗi lần coding

```
TRƯỚC KHI CODE:
□ Đọc file cần sửa (read_file)
□ Đọc MEMORY.md (để nhớ context)
□ Đọc CODING_GUIDELINES.md (để nhớ quy tắc)
□ Tự tranh luận 5 câu hỏi
□ Git commit checkpoint

TRONG KHI CODE:
□ Chỉ thêm/sửa code liên quan trực tiếp
□ Không refactor code liền kề
□ Không thêm feature ngoài yêu cầu
□ Dùng style hiện tại (không đổi formatting)

SAU KHI CODE:
□ Test (pytest / manual)
□ Nếu fail → git checkout revert
□ Nếu pass → git commit
□ Update STRUCTURE.md nếu thêm file mới
□ Update MEMORY.md nếu có quyết định mới
```
