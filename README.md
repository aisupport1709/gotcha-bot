# Gotcha Bot!

Trò chơi giải đố phản xạ: bạn đặt bẫy ẩn trên bản đồ để chặn một con AI đang tìm đường tới đích. AI ghi nhớ mọi cái bẫy nó từng trúng, mỗi vòng lại chạy nhanh hơn và đánh hơi bẫy giỏi hơn — xem bạn cầm cự được bao nhiêu vòng trước khi nó khôn hơn bạn.

A puzzle game where you place hidden traps to stop a pathfinding AI. The AI memorizes every trap it hits, gets faster and sharper each round — see how long you can outsmart it.

## Tính năng / Features

- Chơi ngay trên trình duyệt điện thoại, không cần cài đặt — 100% client-side, không backend
- Đa ngôn ngữ: Tiếng Việt, English, 中文 (tự nhận diện ngôn ngữ thiết bị)
- Bản đồ sinh tường ngẫu nhiên mỗi ván
- AI tìm đường bằng BFS, có bộ nhớ và giác quan tăng dần theo vòng
- Lưu kỷ lục bằng localStorage

## Cấu trúc / Structure

```
└── public/
    ├── index.html      # Toàn bộ game (HTML + CSS + JS trong 1 file)
    ├── manifest.json   # Web app manifest (tên, icon, "Add to Home Screen")
    └── icons/          # App icon các cỡ (favicon, apple-touch-icon, 192/512 PNG, SVG gốc)
```

## Chạy thử local / Run locally

Chỉ cần mở `public/index.html` bằng trình duyệt, hoặc:

```bash
npx serve public
```

## Tùy biến / Customize

- Đổi tên game: sửa hằng số `BRAND` ở đầu `<script>` trong `public/index.html`
- Thêm ngôn ngữ: thêm 1 khối mới vào object `I18N` và 1 nút vào `#langs`
- Chỉnh độ khó: các hàm `senseChance()` (giác quan AI) và `stepMs()` (tốc độ AI)
