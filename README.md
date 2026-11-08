# dsh-plugin-bundle (Phiên bản Tiếng Việt)

[Tiếng Việt](./README.md) | [中文](./README.zh.md)


Bộ gói plugin mở rộng dành cho **DeepSeek Harness (DSH)**. Mỗi thư mục có thể được cài đặt độc lập bằng chỉ thị `path:`.

| Thư mục | Nội dung |
|---|---|
| [`dsh-llm-antigravity-acp`](./dsh-llm-antigravity-acp) | Sử dụng CLI chính thức cục bộ `agy acp` để tích hợp Google Antigravity thành nhà cung cấp mô hình cấp 1 (first-class model provider) trong DSH. Trạng thái đăng nhập được lưu giữ an toàn bên trong tiến trình chính thức của Google, plugin không lưu trữ khoá/token và không chuyển tiếp yêu cầu qua bất kỳ cổng trung gian (gateway) nào. |
| [`agy-context-unlock`](./agy-context-unlock) | Tập lệnh mở khóa ngữ cảnh cục bộ (tùy chọn). Nâng cửa sổ ngữ cảnh mặc định từ 256K lên khoảng 1M token (983.040 tokens) và gỡ bỏ giới hạn độ dài tin nhắn người dùng. Tập lệnh trực tiếp vá tệp nhị phân `agy` cục bộ, không đi kèm trong gói cài đặt tự động của plugin. |

## Cài đặt plugin

```sh
dsh plugin --profile web add "git+https://github.com/shivertuan16-hash/dsh-plugin.git#main&path:/dsh-llm-antigravity-acp"
```

Hoặc cài đặt từ thư mục cục bộ sau khi clone:

```sh
dsh plugin --profile web add ./dsh-llm-antigravity-acp
```

Tài liệu giao thức: [Agent Client Protocol (ACP)](https://agentclientprotocol.com/get-started/introduction).  
Tài liệu sản phẩm `agy acp`: [Antigravity CLI ACP](https://antigravity.google/docs/cli/acp/).

## Cộng đồng

Dự án được mã nguồn mở và chia sẻ tại cộng đồng [LINUX DO](https://linux.do). Xin chân thành cảm ơn các bạn trong cộng đồng đã trao đổi, đóng góp ý kiến và phản hồi.
