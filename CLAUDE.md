# Gotcha Bot!

Trò chơi giải đố (puzzle) client-side thuần HTML/CSS/JS: người chơi đặt bẫy ẩn
trên lưới để chặn một con AI dò đường (BFS) tới đích. AI nhớ mọi bẫy nó từng
trúng và mỗi vòng chạy nhanh hơn, "đánh hơi" bẫy giỏi hơn. Không backend,
không build step — chạy thẳng trong trình duyệt.

## Cấu trúc file

```
└── public/
    ├── index.html      # Toàn bộ game: HTML + CSS + JS trong 1 file, không phụ thuộc ngoài
    ├── manifest.json   # Web app manifest (tên, theme color, icon, standalone display)
    └── icons/          # icon.svg (nguồn) + PNG xuất ra: favicon 16/32, apple-touch-icon 180,
                         # icon-192, icon-512 (dùng cho manifest / "Add to Home Screen")
```

Không dùng backend, không build step, không phụ thuộc Firebase — chỉ là site
tĩnh thuần HTML, có thể host ở bất kỳ static hosting nào (GitHub Pages, Netlify,
Vercel, hoặc mở file trực tiếp).

Toàn bộ logic game nằm trong thẻ `<script>` của `public/index.html`:
- `I18N` object: bảng dịch theo ngôn ngữ (`vi`, `en`, `zh`)
- `bfs()`: tìm đường cho AI, tránh tường + bẫy đã biết (`memory`) + bẫy vừa "ngửi thấy" (`sensed`)
- `senseChance()` / `stepMs()`: độ khó tăng dần theo `round` (giác quan & tốc độ AI)
- `genWalls()`: sinh tường ngẫu nhiên mỗi ván, đảm bảo luôn có đường đi (retry bằng BFS)
- State lưu qua `localStorage`: `gb_best` (kỷ lục), `gb_lang` (ngôn ngữ đã chọn)

## Quy ước i18n

- 3 ngôn ngữ: `vi`, `en`, `zh` — object `I18N` trong `public/index.html`, mỗi khối chứa toàn bộ text UI + mảng thoại ngẫu nhiên (`dieMsgs`, `senseMsgs`).
- Tự nhận diện ngôn ngữ qua `navigator.language`, ưu tiên `localStorage.gb_lang` nếu người dùng đã chọn thủ công.
- Thêm ngôn ngữ mới: thêm 1 khối trong `I18N` (đủ tất cả key hiện có) + 1 nút trong `#langs` ở HTML.
- Không tách file dịch riêng — cố tình gộp 1 file để giữ game "single-file, no build".

## Cách chạy / deploy

Đây là site tĩnh 100% — chỉ cần serve thư mục `public/` bằng bất kỳ static host
nào (GitHub Pages, Netlify, Vercel...), hoặc mở thẳng `public/index.html` bằng
trình duyệt. Không cần backend, build step, hay Firebase.

```bash
npx serve public
```
