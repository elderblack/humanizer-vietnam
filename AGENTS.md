# Hướng dẫn đóng góp (cho người và agent)

Tệp này giải thích cách sửa Humanizer tiếng Việt mà không làm hỏng gói hay prompt.

## Repo chứa gì

Đây là một agent skill viết bằng Markdown. `SKILL.md` là prompt mà agent đọc. Repo không có bước build.

Giữ skill dùng được trên nhiều agent. Không viết chỉ dẫn chỉ chạy được trên một hai công cụ.

## Các tệp chính

- `SKILL.md` là nguồn chuẩn và là tệp skill duy nhất. Gồm YAML metadata, phần giải thích vì sao văn AI nghe như vậy, và các mẫu đánh số chia thành tám nhóm, xếp theo độ mạnh và độ phổ biến.
- `README.md` hướng dẫn cài đặt, cách dùng và bảng mẫu.
- `CHANGELOG.md` ghi các bản phát hành, mới nhất ở trên. Ghi chú cũ giữ số mẫu của bản đó.
- `.claude-plugin/plugin.json` và `.claude-plugin/marketplace.json` cho Claude Code.
- `.cursor-plugin/plugin.json` cho Cursor. Không thêm trường `skills`, để Cursor tự nạp `SKILL.md` ở gốc.
- `package.json` biến repo thành gói pi. Không thêm trường `version`.
- `agents/openai.yaml` chứa tên hiển thị và câu lệnh mặc định cho agent kiểu OpenAI.
- `scripts/validate-package.py` kiểm tra các tệp gói và giá trị dùng chung.

## Quy tắc khi sửa

Giữ `SKILL.md` và `README.md` khớp nhau.

- **Mẫu:** Đánh số từ 1, không bỏ số, mạnh và phổ biến trước. Chỉ thêm mẫu mới khi không mẫu nào có sẵn bao được nó; ưu tiên gộp vào mẫu có sẵn. Thêm, bớt hay đánh số lại thì cập nhật bảng README, tiêu đề "Các N mẫu" trong README, và mọi tham chiếu §. Script kiểm tra tự đếm số mẫu từ tiêu đề và so tên với bảng README.
- **Phiên bản:** Giữ cùng một số phiên bản ở `metadata.version` trong `SKILL.md`, tiêu đề đầu tiên của `CHANGELOG.md`, `.claude-plugin/plugin.json` và `.cursor-plugin/plugin.json`.
- **Mô tả:** Các manifest dùng câu đầu tiên trong phần description của `SKILL.md`.
- **Độ dài:** Agent đọc toàn bộ `SKILL.md` mỗi lần dùng. Script giới hạn 9.000 tiếng (tính theo khoảng trắng; tiếng Việt tốn nhiều "từ" hơn tiếng Anh cho cùng một ý). Thay đổi làm dài thêm phải đáng giá.
- **Lịch sử:** Ghi một dòng ngắn vào `CHANGELOG.md` cho mọi thay đổi hành vi.
- **Kiểm tra:** Trước khi phát hành, chạy `python3 scripts/validate-package.py`, `npx skills add . --list` và `claude plugin validate .`.

## Ví dụ trong skill

- Ví dụ "Trước" phải nghe như văn AI tiếng Việt thật, không phải bản dịch từ ví dụ tiếng Anh.
- Ví dụ "Sau" không được thêm sự thật không có trong bản "Trước". Nếu bản "Sau" cần chi tiết để minh họa, ghi chú rằng chỉ viết vậy khi nguồn có chi tiết đó.
- Ví dụ "Sau" phải sạch các mẫu khác. Một bản "Sau" còn "Điều này" hay "một cách" sẽ dạy sai.
- Tránh thông tin hành chính dễ lỗi thời (tên tỉnh, cấp huyện sau sáp nhập).

## Văn phong

Viết tiếng Việt rõ ràng trong prompt, tài liệu, mô tả và thông báo lỗi.

- Ý chính đặt trước.
- Dùng từ thông dụng và câu chủ động.
- Câu và đoạn ngắn.
- Một khái niệm dùng một tên.
- Dùng "phải" cho yêu cầu bắt buộc.
- Giữ nguyên định danh, lệnh, đường dẫn, trích dẫn và cụm từ trong danh sách "Để ý".
