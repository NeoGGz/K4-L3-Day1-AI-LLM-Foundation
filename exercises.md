# K4 — Ngày 1: Bài Tập & Phản Ánh
## Khám Phá LLM API | Phiếu Thực Hành

**Thời lượng:** 4 tiếng
**Cách làm:** Trả lời từng câu ngay sau khi hoàn thành block tương ứng —
đừng để dồn hết về cuối buổi. Thay dòng `*Câu trả lời của bạn*` bằng câu
trả lời thật (chấm tự động sẽ đếm số câu đã trả lời).

---

## Block 1 — API Cơ Bản (trả lời sau Checkpoint 1)

### Câu 1.1 — Độ nhạy của temperature
Gọi `call_openai` với temperature 0.0, 0.5, 1.0 và 1.5 dùng prompt
**"Hãy kể cho tôi một sự thật thú vị về Việt Nam."**

**Bạn nhận thấy quy luật gì qua bốn phản hồi?** (2–3 câu)
> *temp = 0 sẽ cho ra kết quả nhất quán hơn, với temp = 0.5, 1 thì sẽ cho kết quả đa dạng hơn, với temp = 1.5 thì sẽ cho nhiều kết quả lan man*

### Câu 1.2 — Chọn temperature cho sản phẩm
**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> *Để hỗ trợ khách hàng, temp sẽ được đặt ở 0 đến ~0.3, bởi cần sự chính xác cao*

### Câu 1.3 — Đánh đổi chi phí
Kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người gọi API 3 lần,
mỗi lần trung bình ~350 token đầu ra.

**Ước tính GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này? Nêu một
trường hợp GPT-4o xứng đáng với chi phí và một trường hợp nên dùng mini:**
> *GPT-4o đắt hơn gấp 16.7 lần so với GPT-4o-mini. GPT-4o xứng đáng hơn trong trường hợp cần thông tin, suy luận có độ chính xác cao. Còn bản mini trong trường hợp CSKH cơ bản...*

---

## Block 2 — System Prompt & Token (trả lời sau Checkpoint 2)

### Câu 2.1 — Sức mạnh của persona
Gọi `chat_with_system_prompt` hai lần với cùng câu hỏi
**"Giải thích blockchain là gì?"** nhưng hai system prompt khác nhau:
- "Bạn là giáo viên tiểu học, giải thích thật đơn giản cho trẻ 8 tuổi."
- "Bạn là chuyên gia tài chính, trả lời chuyên sâu bằng thuật ngữ kỹ thuật."

**Hai phản hồi khác nhau như thế nào (độ dài, từ vựng, ví dụ)? System prompt
ảnh hưởng đến hành vi model ra sao?** (3–4 câu)
> *Phản hồi của dòng prompt đầu ngắn hơn so với prompt 2, từ ngữ cũng dễ hiểu hơn thay vì những từ ngữ chuyên ngành. Prompt ảnh hưởng lớn đến model, định hình vai trò của model cũng như kiến thức.*

### Câu 2.2 — tiktoken vs đếm từ
Chọn một đoạn văn tiếng Việt ~100 từ. So sánh số token theo `count_tokens`
(tiktoken) với ước lượng `số từ / 0.75` mà Part 1 đã dùng.

**Hai con số chênh nhau bao nhiêu phần trăm? Vì sao tiếng Việt thường tốn
nhiều token hơn tiếng Anh cùng độ dài?**
> *Số token chênh nhau khá nhiều, khoảng 40%, LLM tối ưu cho tiếng Anh do vậy tiếng Việt sẽ tốn nhiều token hơn bởi vì phải chia nhỏ các từ tiếng Việt thành các sub-word tokens hơn*

---

## Block 3 — Streaming & Độ Bền (trả lời sau Checkpoint 3)

### Câu 3.1 — Trải nghiệm người dùng với streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì
non-streaming lại phù hợp hơn?** (1 đoạn văn)
> *Streaming quan trọng hơn trong trường hợp là trò chuyện trực tiếp, non streaming phù hợp hơn với tác vụ chạy ngầm*

### Câu 3.2 — Vì sao backoff theo cấp số nhân?
**So với delay cố định (ví dụ luôn chờ 1 giây), exponential backoff có lợi
thế gì khi API bị quá tải? Điều gì xảy ra nếu hàng nghìn client cùng retry
với delay cố định giống nhau?**
> *Lợi thế của exponential backoff là khi API bị quá tải, việc giãn các khoảng thử lại sẽ giúp cho server hạ tải và phục hồi thay vì cứ mỗi 1s retry 1 lần, có khả năng khiến server sập.*

---

## Block 4 — Mini-Project (trả lời sau Checkpoint 4)

### Câu 4.1 — Thiết kế persona
**Bạn chọn persona gì cho trợ lý của mình? Viết lại system prompt đó và giải
thích 1–2 lựa chọn từ ngữ quan trọng trong prompt (ví dụ: vì sao yêu cầu
"trả lời ngắn gọn", vì sao chỉ định ngôn ngữ...):**
> *Giải thích khái niệm LLM với từ ngữ dễ hiểu cho người mới tiếp cận, bằng tiếng Việt. Dùng "từ ngữ dễ hiểu" để câu trả lời k chứa các từ ngữ chuyên ngành, dễ hiểu cho người mới tiếp cận, bằng Tiếng Việt để mặc định câu trả lời bằng ngôn ngữ đó.*

### Câu 4.2 — Hạn chế & cải thiện
**Trợ lý của bạn hiện có hạn chế lớn nhất là gì (ví dụ: history chỉ 3 lượt,
không có bộ nhớ dài hạn, không kiểm duyệt nội dung...)? Đề xuất một cải
thiện cụ thể và mô tả ngắn cách triển khai:**
> *Hạn chế: Chatbot hiện chỉ giữ lại 3 cuộc hội thoại gần nhất (history = history[-6:]), khiến nó bị "quên" ngữ cảnh và thông tin ban đầu khi cuộc trò chuyện kéo dài. Cải thiện: Áp dụng kỹ thuật Summary Memory (Tóm tắt hội thoại). Khi cuộc hội thoại vượt quá 3 lượt, dùng LLM tóm tắt các lượt hội thoại cũ thành một đoạn ngắn và nhét đoạn tóm tắt đó vào system prompt thay vì xóa bỏ hoàn toàn.*

---

## Danh Sách Kiểm Tra Nộp Bài

- [ ] `python grade.py` — xem điểm tự động, mục tiêu ≥ 75/100
- [ ] Cả 4 checkpoint pytest đều pass
- [ ] Tất cả 9 câu trong file này đã được trả lời
- [ ] Đã copy bài làm vào folder `solution/`, push lên fork và dán link trên trang bài Lab ở VLearn trước 23:59 ngày 11/09/2026
