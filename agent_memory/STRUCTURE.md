# STRUCTURE.md

> **LƯU Ý:** LUÔN CẬP NHẬT file này khi có thay đổi cấu trúc thư mục hoặc chức năng của file/folder trong project.

## Moodle-Docker Structure

```text
moodle-docker/
├── .git/                      # Git metadata
├── .github/                   # GitHub Actions (CI workflows)
├── assets/                    # File cấu hình phụ trợ (apache, faildumps...)
├── bin/                       # Scripts khởi chạy (bash scripts như moodle-docker-compose)
├── tests/                     # Automated tests cho chính repo này
├── agent_memory/              # Thư mục lưu trữ bối cảnh AI Agent (MEMORY, STRUCTURE, CODING_GUIDELINES)
│   ├── MEMORY.md
│   ├── STRUCTURE.md
│   └── CODING_GUIDELINES.md
├── docker-compose.yml         # Cấu hình gom chung cho môi trường (được agent tạo)
├── base.yml                   # Cấu hình Docker cơ bản gốc
├── db.*.yml                   # Các cấu hình chia theo loại database (pgsql, mariadb, oracle...)
├── service.mail.yml           # Cấu hình cho Mailpit
├── webserver.port.yml         # Cấu hình mapping port web
├── README.md                  # Hướng dẫn chính của repo
└── LICENSE
```

### Component Details
- **docker-compose.yml**: Chứa cấu hình gộp (PostgreSQL, PHP 8.3, Mailpit, Selenium) dùng để start/stop môi trường Moodle chỉ với 1 lệnh `docker compose up -d`.
- **bin/moodle-docker-compose**: Script bash cũ hỗ trợ wrap nhiều tham số `-f` (hiện tại có thể dùng `docker-compose.yml` để thay thế).
- **agent_memory/**: Lưu lại tri thức của bot về luồng xử lý và quy tắc làm việc trên repo này.
