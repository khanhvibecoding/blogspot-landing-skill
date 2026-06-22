# Blogspot Landing Agent for Codex

Tạo landing page một trang cho Blogger/Blogspot và xuất template XML có thể dán trực tiếp vào Blogger.

Đầu ra gồm landing-spec.json, landing-template.xml, preview.html, qa-report.json và change-log.md.

## Cài từ GitHub

### 1. Tải ZIP

Trên GitHub, nhấn Code → Download ZIP, rồi giải nén file. Tìm thư mục có file SKILL.md; đó là thư mục skill cần cài.

### 2. Chép vào Codex

Đóng Codex trước khi cài.

macOS / Linux:

    mkdir -p ~/.codex/skills
    cp -R /duong-dan-den/blogspot_landing_agent ~/.codex/skills/blogspot-landing-agent

Windows PowerShell:

    New-Item -ItemType Directory -Force "$HOME\.codex\skills"
    Copy-Item -Recurse "C:\duong-dan-den\blogspot_landing_agent" "$HOME\.codex\skills\blogspot-landing-agent"

Mở lại Codex. Thư mục được cài phải chứa trực tiếp file SKILL.md, không được lồng hai cấp thư mục.

## Dùng trong Codex

Mở workspace sản phẩm và yêu cầu Codex bằng ngôn ngữ tự nhiên, ví dụ:

    Dùng Blogspot Landing Agent để tạo landing page Blogger cho tool tạo video AI.
    Tên: K Studio.
    Khách hàng: creator YouTube, TikTok và Reels.
    CTA: Mua qua Zalo https://zalo.me/0858566936.
    Giá: 700k, gồm source code, video hướng dẫn và nhóm Zalo hỗ trợ.

Để chỉnh sửa bản có sẵn:

    Dùng Blogspot Landing Agent, cập nhật landing Blogger hiện tại:
    - thêm gallery ảnh sản phẩm
    - tách QR thanh toán thành section riêng, không crop ảnh
    - kiểm tra lại XML và preview trước khi giao file

## Import lên Blogger

1. Mở landing-template.xml và copy toàn bộ nội dung.
2. Trong Blogger, vào Chủ đề → menu cạnh Tùy chỉnh → Chỉnh sửa HTML.
3. Sao lưu theme cũ.
4. Thay toàn bộ mã bằng nội dung landing-template.xml, sau đó lưu.

Mở preview.html để xem trước. Chỉ import khi qa-report.json có passed là true.

## Lỗi ký tự Blogger

Blogger có thể mã hóa ký tự trong CSS. Ví dụ tick đôi khi hiện thành:

    &#10003;

Không dùng HTML entity trong CSS pseudo-element:

    content: "&#10003;";

Dùng CSS Unicode escape:

    content: "\\2713";

Validator của skill sẽ báo lỗi khi phát hiện HTML entity trong CSS content. Quy tắc này cũng áp dụng cho mũi tên, bullet, icon và mọi ký tự tạo bằng ::before hoặc ::after.

## Yêu cầu

- Python 3 để chạy generator và validator.
- Blog Blogger để import template.
- Thông tin sản phẩm thật: CTA, giá, ảnh, QR và nội dung cần hiển thị.

