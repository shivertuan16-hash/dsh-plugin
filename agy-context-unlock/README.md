# agy-context-unlock (Bản Tiếng Việt)

[Tiếng Việt](./README.md) | [中文](./README.zh.md)


Mở rộng cửa sổ ngữ cảnh của Google Antigravity chính thức trên máy từ mặc định 256K lên khoảng 1M token (983.040 tokens), đồng thời gỡ bỏ giới hạn cắt tỉa 64K tokens (192.000 bytes) cho một tin nhắn người dùng đơn lẻ (`USER_INPUT`). Hỗ trợ macOS (arm64 / x86-64), Linux (x86-64 / arm64) và Windows (x86-64 / arm64), yêu cầu `agy >= 1.5.0`.

Thư mục này không nằm trong gói cài đặt tự động của plugin DSH. Việc chạy tập lệnh tại đây sẽ trực tiếp điều chỉnh tệp nhị phân chính thức của `agy`. Khi `agy` hoặc phiên bản Antigravity Desktop nâng cấp, tệp nhị phân mới sẽ quay về 256K và bạn chỉ cần chạy lại tập lệnh một lần nữa.

Plugin [`dsh-llm-antigravity-acp`](../dsh-llm-antigravity-acp) có cơ chế `autoPatch` tự động tìm kiếm tệp tại đường dẫn:
- **macOS / Linux:** `~/.gemini/antigravity/tools/agy-patch.py`
- **Windows:** `%USERPROFILE%\.gemini\antigravity\tools\agy-patch.py`

Khi bạn đặt tệp `agy-patch.py` vào đường dẫn trên, plugin sẽ tự động kiểm tra và thực hiện vá khi chưa mở khóa. Nếu không tìm thấy tập lệnh, cửa sổ ngữ cảnh giữ nguyên 256K mặc định an toàn.

---

## 1. Mở khóa cho Antigravity CLI (`agy`) trong terminal

Trước tiên hãy kiểm tra phiên bản `agy --version` (yêu cầu `>= 1.5.0`, nếu là bản cũ hơn hãy nâng cấp bằng `agy update`). Tắt toàn bộ các tiến trình `agy` đang chạy và thực hiện:

### macOS / Linux:

```sh
# Chạy thử nghiệm kiểm tra các cổng (không ghi file):
python3 agy-patch.py --binary ~/.local/bin/agy --dry-run

# Áp dụng vá trực tiếp (tự động sao lưu bản gốc thành .bak):
python3 agy-patch.py --binary ~/.local/bin/agy --in-place
```

### Windows (PowerShell):

```powershell
# Chạy thử nghiệm kiểm tra:
python agy-patch.py --binary "$env:LOCALAPPDATA\agy\bin\agy.exe" --dry-run

# Áp dụng vá trực tiếp (tự động tạo bản sao lưu agy.exe.bak):
python agy-patch.py --binary "$env:LOCALAPPDATA\agy\bin\agy.exe" --in-place
```

*Ghi chú: Nếu bỏ qua tham số `--binary`, tập lệnh sẽ tự động tìm theo đường dẫn mặc định của hệ điều hành. Tham số `--dry-run` chỉ kiểm tra tình trạng các cổng bảo vệ; `--in-place` sẽ tự động tạo file sao lưu `.bak` trước khi vá.*

---

## 2. Mở khóa cho ứng dụng Antigravity Desktop

Thoát hoàn toàn ứng dụng Antigravity Desktop, sau đó chạy:

### macOS:

```sh
python3 agy-patch.py \
  --binary "/Applications/Antigravity.app/Contents/Resources/bin/language_server" \
  --in-place --no-backup
```

### Windows (PowerShell):

```powershell
python agy-patch.py `
  --binary "$env:LOCALAPPDATA\Programs\Antigravity\resources\bin\language_server.exe" `
  --in-place
```

Khởi động lại ứng dụng Antigravity Desktop để sử dụng tệp nhị phân đã mở khóa.

---

## 3. Cơ chế tự động mở khóa lại sau khi cập nhật

- **Windows / Linux:** Khi sử dụng kèm plugin DSH `dsh-llm-antigravity-acp`, plugin đã tích hợp sẵn cờ `autoPatch` tự động kiểm tra và vá lại nhị phân trước mỗi lần khởi chạy phiên `agy acp`.
- **macOS:** Nếu đồng thời sử dụng CLI terminal và bản Desktop, bạn có thể sử dụng `agy-autopatch.py` kết hợp với `launchd` để tự động vá lại ngay khi có bản cập nhật mới.
