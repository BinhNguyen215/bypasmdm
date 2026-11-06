# Bypass MDM (macOS)

Script hỗ trợ bỏ qua MDM (Mobile Device Management) và tạo tài khoản quản trị trên macOS.
Có thể chạy trong **Recovery Mode** hoặc trong macOS đã cài đặt sẵn.

- Repo: <https://github.com/BinhNguyen215/bypasmdm>
- Script: [`mdm.sh`](mdm.sh)

## Cài đặt nhanh

Mở **Terminal** trên macOS và chạy:

```bash
curl https://raw.githubusercontent.com/BinhNguyen215/bypasmdm/main/mdm.sh -o test.sh && chmod +x ./test.sh && ./test.sh
```

Lệnh trên tải `mdm.sh` từ nhánh `main`, cấp quyền thực thi rồi chạy luôn menu tương tác.

## Chạy thủ công

```bash
git clone https://github.com/BinhNguyen215/bypasmdm.git
cd bypasmdm
chmod +x mdm.sh
./mdm.sh
```

## Menu chức năng

| # | Chức năng | Mô tả | Môi trường |
|---|-----------|-------|------------|
| 1 | Bypass on Recovery | Tạo user mới (mặc định `MAC` / `1234`), chặn `deviceenrollment.apple.com`, `mdmenrollment.apple.com`, `iprofiles.apple.com` và xoá cấu hình MDM | Recovery Mode |
| 2 | Disable Notification (SIP) | Xoá các file `.cloudConfig*` để tắt thông báo cài đặt profile | macOS, cần SIP đã tắt |
| 3 | Disable Notification (Recovery) | Như trên nhưng thao tác trực tiếp trên volume `Macintosh HD` | Recovery Mode |
| 4 | Check MDM Enrollment | Chạy `sudo profiles show -type enrollment` để kiểm tra máy còn bị quản lý hay không | macOS |
| 5 | Quit | Thoát script | — |

### Chức năng 1 — Bypass on Recovery

Script sẽ hỏi 3 thông tin (có giá trị mặc định, nhấn Enter để bỏ qua):

- **Full Name** — mặc định `MAC`
- **Username** — mặc định `MAC` (không dấu cách, không ký tự đặc biệt)
- **Password** — mặc định `1234`

Sau đó script tạo tài khoản với `UID 501`, thêm vào nhóm `admin`, chặn các host MDM trong `/etc/hosts` và vô hiệu hoá cấu hình MDM.

### Chức năng 4 — Check MDM Enrollment

Câu lệnh thành công sẽ in ra profile enrollment. Thông báo lỗi (ví dụ *"There are no profiles installed on this system"*) nghĩa là máy **đã sạch MDM**.

## Yêu cầu

- macOS (Intel hoặc Apple Silicon)
- Quyền truy cập **Recovery Mode** cho chức năng 1 và 3
- SIP đã tắt cho chức năng 2 (`csrutil disable`)
- Kết nối mạng để tải script bằng `curl`

## Cấu trúc repo

```
bypasmdm/
├── LICENSE    # Giấy phép MIT
├── README.md  # Tài liệu này
└── mdm.sh     # Script chính
```

## Cảnh báo

- Chỉ sử dụng trên thiết bị **bạn sở hữu**. Bỏ qua MDM trên thiết bị của tổ chức/người khác là hành vi vi phạm pháp luật và điều khoản dịch vụ.
- Thao tác trên hệ thống và Recovery có thể gây **mất dữ liệu** hoặc khiến máy không khởi động được. Hãy sao lưu trước.
- Việc can thiệp có thể làm **mất hiệu lực bảo hành** và hỗ trợ từ Apple.
- Tác giả không chịu trách nhiệm cho bất kỳ thiệt hại nào phát sinh.

## Giấy phép

Phát hành theo giấy phép [MIT](LICENSE) © 2026 BinhNguyen215.
