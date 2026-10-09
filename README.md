# POWER QUIZ – TUG OF WAR

Web game mini bằng HTML, CSS và JavaScript thuần. Chạy trên trình duyệt, có thể triển khai miễn phí bằng GitHub Pages; không cần backend, tài khoản hoặc API key.

## File dự án

- `index.html` — các màn hình và cấu trúc giao diện.
- `style.css` — giao diện responsive, nhân vật chibi CSS và các animation kéo co.
- `game.js` — ngân hàng câu hỏi, đồng hồ, tính điểm, AI, chuyển lượt và điều kiện thắng.

## Chạy thử

Mở `index.html` bằng trình duyệt. Nếu trình duyệt hoặc môi trường máy tính chặn trang HTML mở trực tiếp, có thể chạy một máy chủ tĩnh tại thư mục dự án:

```bash
python3 -m http.server 8000
```

Sau đó mở `http://localhost:8000`.

## Triển khai GitHub Pages

1. Tạo repository, ví dụ `power-quiz-tug-of-war`.
2. Upload `index.html`, `style.css`, `game.js` và `README.md` vào thư mục gốc.
3. Vào **Settings → Pages**.
4. Trong **Build and deployment**, chọn **Deploy from a branch**.
5. Chọn nhánh `main`, thư mục `/(root)` và nhấn **Save**.
6. Mở URL GitHub Pages được cung cấp sau khi deploy.

## Cách chơi

- **Solo Challenge:** mỗi trận chỉ có **12 câu hỏi**. Chọn EASY (AI đúng khoảng 45%), NORMAL (55%) hoặc HARD (65%). Sau mỗi câu của người chơi, Người Khổng Lồ mô phỏng một lượt trả lời dựa trên xác suất của cấp độ đã chọn. Nếu chưa ai chạm vạch đích sau 12 câu, người có lợi thế vị trí thắng; nếu vị trí hòa, so sánh tổng sức mạnh.
- **Two-Player Online:** hai người chơi trên **hai thiết bị riêng** cùng mở trang game. Người thứ nhất chọn **TẠO PHÒNG** và gửi mã 6 chữ số cho người còn lại; người thứ hai nhập mã và chọn **THAM GIA**. Khi kết nối thành công, cả hai nhận cùng câu hỏi và cùng trả lời trong một lượt. Trận online cần kết nối Internet và tải thư viện PeerJS từ CDN; chế độ này dùng PeerJS để thiết lập kết nối ngang hàng.
- Câu trả lời đúng cộng sức mạnh theo độ khó câu hỏi: EASY +10, MEDIUM +20, HARD +30. Câu sai/hết giờ không cộng điểm. Trong chế độ hai người, câu sai còn khiến dấu mốc dịch nhẹ về phía đối thủ.
- Dấu mốc đỏ trên dây, vị trí nhân vật và thanh lợi thế cùng phản ánh trạng thái kéo co. Đạt vạch đích ở ±100 sẽ kết thúc trận.
- Đồng hồ, đáp án, AI và nút chuyển lượt được khóa khi đã xử lý câu trả lời để tránh nhận điểm lặp.

## Thêm câu hỏi

Trong `game.js`, tìm mảng `questions` và thêm object theo cấu trúc:

```js
{
  q: "Nội dung câu hỏi?",
  a: ["Đáp án A", "Đáp án B", "Đáp án C", "Đáp án D"],
  correct: 2, // chỉ số đáp án đúng, bắt đầu từ 0
  topic: "logic", // logic | science | general | math
  difficulty: "easy", // easy | medium | hard
  explain: "Giải thích đáp án."
}
```

Có thể thêm 5 đáp án nếu cần; game tự xáo trộn thứ tự đáp án và hiển thị chữ A–E tương ứng.

## Kiểm tra kỹ thuật

- Đã kiểm tra cú pháp JavaScript bằng `node --check game.js`.
- Đã kiểm tra cú pháp JavaScript bằng `node --check game.js`. Chế độ online dựa vào dịch vụ PeerJS và cần được kiểm thử thực tế trên hai thiết bị sau khi triển khai GitHub Pages.
- Môi trường kiểm thử trình duyệt headless hiện chặn điều hướng đến file/local server theo chính sách của môi trường; vì vậy chưa thể xác nhận bằng thao tác trình duyệt end-to-end trong môi trường này. Vui lòng chạy thử trên Chrome/Safari sau khi mở file hoặc deploy GitHub Pages.

## Lưu ý

- Multiplayer online phụ thuộc vào kết nối Internet, PeerJS CDN và dịch vụ signaling của PeerJS; không hoạt động hoàn toàn offline.
- Nhân vật và hiệu ứng được dựng bằng CSS; Google Fonts chỉ là tùy chọn.
