# Humanizer tiếng Việt

[English below](#english)

Humanizer tiếng Việt là một agent skill giúp văn bản tiếng Việt do AI viết đọc như người thật viết, mà không đổi điều văn bản muốn nói. Skill chuyển thể từ [Humanizer](https://github.com/blader/humanizer) của Siqi Chen, vốn dựa trên trang [Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) của Wikipedia, rồi bổ sung những dấu hiệu chỉ có trong tiếng Việt: văn dịch, Hán-Việt rỗng, cặp từ đôi, xưng hô lệch, đoạn kết "Tóm lại". Skill chạy được trong Claude Code, Codex, Cursor và mọi agent hỗ trợ skill.

**Trước:**
> Chắc chắn rồi! Trong thời đại số hiện nay, làm việc nhóm không chỉ là một kỹ năng, mà còn là chìa khóa dẫn đến thành công. 🚀 Hôm nay, chúng tôi vô cùng hào hứng giới thiệu tính năng **Bản nháp chung**, đánh dấu một bước ngoặt trong hành trình kiến tạo trải nghiệm cộng tác. Việc chỉnh sửa tài liệu giờ đây được thực hiện một cách nhanh chóng và hiệu quả bởi nhiều người cùng lúc. Bên cạnh đó, bình luận luôn được gắn chính xác vào câu được nhắc đến. Đặc biệt, tính năng hoàn toàn miễn phí! Tóm lại, Bản nháp chung sẽ mang đến cho bạn trải nghiệm làm việc nhóm toàn diện và vượt trội. Hãy trải nghiệm ngay hôm nay nhé!

**Sau:**
> Bản nháp chung ra mắt hôm nay. Giờ hai người có thể sửa cùng một tài liệu và thấy thay đổi của nhau ngay khi gõ. Bình luận dính vào đúng câu nó nhắc tới, kể cả khi đoạn văn xung quanh đã đổi. Tính năng miễn phí cho mọi gói.

Skill này sửa văn cho người đọc. Nó không nhằm qua mặt công cụ phát hiện AI, và các công cụ đó vẫn có thể bắt được kết quả.

## Năm dấu hiệu mạnh nhất

Gặp một trong năm dấu hiệu này là skill sửa ngay:

1. **Không phải X mà là Y:** "Đây không chỉ là một chiếc điện thoại, mà là một tuyên ngôn."
2. **Câu chốt một dòng:** "Và đó chính là điều tạo nên sự khác biệt."
3. **Câu nói nghe có vẻ sâu sắc:** "Suy cho cùng, điều thực sự quan trọng là..."
4. **Câu dẫn vòng vo:** "Trong thời đại số hiện nay...", "Hãy cùng khám phá..."
5. **Cãi với người không tồn tại:** "Tôi không nói rằng X, nhưng..."

Tổng cộng skill kiểm tra [32 mẫu](#các-32-mẫu).

## Cài đặt

Cài xong, gọi bằng `/humanizer-vietnam`.

### Claude Code

```text
/plugin marketplace add elderblack/humanizer-vietnam
/plugin install humanizer-vietnam@humanizer-vietnam
```

Plugin cần Claude Code 2.1.142 trở lên. Bản cũ hơn thì dùng:

```bash
npx skills add elderblack/humanizer-vietnam --global --agent claude-code
```

### Codex

```bash
npx skills add elderblack/humanizer-vietnam --global --agent codex
```

### pi

```bash
pi install git:github.com/elderblack/humanizer-vietnam
```

### Claude.ai và Claude Desktop

Tải repo về dạng ZIP (**Code → Download ZIP**) rồi tải lên làm skill trong phần Settings.

### Agent khác

```bash
npx skills add elderblack/humanizer-vietnam --global --agent '*'
```

Lệnh này cài cho mọi agent mà Skills CLI hỗ trợ, gồm Gemini CLI, GitHub Copilot và Windsurf. Bỏ `--global` để chỉ cài cho dự án hiện tại. Với agent mà Skills CLI chưa biết, chép `SKILL.md` vào thư mục skill của agent đó.

### Dùng chung với Humanizer bản gốc

Hai skill có tên khác nhau (`humanizer` và `humanizer-vietnam`) nên cài cùng lúc được. Văn tiếng Việt thì gọi `/humanizer-vietnam`, văn tiếng Anh thì gọi `/humanizer`.

## Cách dùng

Gọi trực tiếp:

```text
/humanizer-vietnam

[dán văn bản vào đây]
```

Hoặc nói bình thường:

```text
Sửa giúp mình đoạn này cho bớt giọng AI: [văn bản]
```

Sửa một tệp:

```text
Sửa văn trong docs/bai-ra-mat.md cho tự nhiên hơn
```

Skill đọc toàn bộ tệp trước khi sửa, chỉ sửa văn xuôi, để nguyên code, dữ liệu, frontmatter và đường dẫn, rồi báo đã rà bao nhiêu phần.

### Giữ giọng của bạn

Muốn bản viết lại giống giọng bạn, đưa kèm một mẫu văn:

```text
/humanizer-vietnam

Đây là mẫu văn của mình để bắt giọng:
[dán 2-3 đoạn bạn tự viết]

Giờ sửa đoạn này:
[dán văn bản AI]
```

Skill sẽ theo nhịp câu, cách chọn từ, dấu câu, cách xưng hô, trợ từ cuối câu ("nhé", "nha", "á") và cả thói quen chen tiếng Anh của bạn.

## Cách hoạt động

Mô hình ngôn ngữ viết ra chữ có khả năng xuất hiện cao nhất, nên mặc định nó chọn cách nói hợp với nhiều người đọc nhất. Người viết thật chọn cho một người đọc và một chủ đề. Mỗi dấu hiệu skill tìm là một dạng của lựa chọn mặc định đó.

Với tiếng Việt còn một lớp nữa: mô hình học tiếng Việt qua rất nhiều văn bản dịch, nên nó hay viết tiếng Việt bằng ngữ pháp tiếng Anh ("Việc sử dụng...", "được phát triển bởi", "Điều này cho thấy", "một cách hiệu quả").

Skill đánh dấu mọi dấu hiệu, viết nháp, soát nháp với danh sách mẫu và với các khẳng định gốc, rồi viết bản cuối. Nó giữ mọi khẳng định của bản gốc và không bịa thêm chi tiết.

Nhiều mẫu đã có trong công văn, báo chí chính luận và bài văn nhà trường từ trước khi có AI. Skill biết điều đó: với công văn và văn bản pháp quy, nó giữ thể thức và chỉ gỡ đồ thừa.

## Các 32 mẫu

Mẫu xếp từ mạnh và phổ biến nhất đến yếu nhất. Năm mẫu đầu được sửa ngay lần đầu gặp. Mẫu ghi *yếu khi đứng một mình* chỉ được sửa khi đi cùng các dấu hiệu khác trong cùng đoạn.

### A. Dàn dựng thay vì nói thẳng

| # | Mẫu | Trước | Sau |
|---|-----|-------|-----|
| 1 | **Không phải X mà là Y** | "không chỉ là X, mà là Y", "Điều này không có nghĩa là X. Nó có nghĩa là Y." | Nói thẳng ý chính |
| 2 | **Câu chốt một dòng và câu ngắt kịch tính** | "Và đó chính là chìa khóa."; "Không kế hoạch. Không đường lui." | Cắt câu lặp ý; gộp câu cụt thành một ý cụ thể |
| 3 | **Câu nói nghe có vẻ sâu sắc** | "Suy cho cùng...", "X là tấm gương phản chiếu Y" | Thay bằng khẳng định cụ thể |
| 4 | **Câu dẫn vòng vo trước khi vào ý** | "Trong thời đại số hiện nay", "Hãy cùng tìm hiểu nhé!" | Bỏ câu dẫn, vào ý luôn |
| 5 | **Cãi với người không tồn tại** | "Tôi không nói rằng...", "Có thể bạn nghĩ... nhưng" | Bỏ phản bác không ai nêu |

### B. Nhịp theo công thức

| # | Mẫu | Trước | Sau |
|---|-----|-------|-----|
| 6 | **Bộ ba gượng ép** | "cảm hứng, kiến thức và góc nhìn mới" | Dùng đúng số mục nghĩa cần |
| 7 | **Cặp từ đôi chất đống** | "chuyên nghiệp và tận tâm", "nhanh chóng và hiệu quả" | Giữ một từ, hoặc thay bằng chi tiết |
| 8 | **Mở câu lặp lại** | "Bên cạnh đó... Ngoài ra... Đặc biệt..." | Bỏ từ nối, gộp câu |
| 9 | **Gạch ngang ở khắp nơi** (*yếu khi đứng một mình*) | "Chính sách — công bố bất ngờ — ảnh hưởng..." | Dùng chấm, phẩy, hai chấm, ngoặc đơn |
| 10 | **Rào đón chồng chất** (*yếu khi đứng một mình*) | "có thể phần nào ở một mức độ nào đó" | Giữ từ rào mà nguồn ủng hộ |

### C. Văn dịch và Hán-Việt rỗng

| # | Mẫu | Trước | Sau |
|---|-----|-------|-----|
| 11 | **Danh từ hóa bằng "việc" và "sự"** | "Việc sử dụng... giúp cho sự phối hợp..." | Để động từ làm vị ngữ, nêu ai làm |
| 12 | **Động từ rỗng và "một cách"** | "tiến hành thực hiện việc kiểm tra một cách toàn diện" | "kiểm tra toàn bộ" |
| 13 | **Bị động kiểu dịch: "được... bởi"** | "được phát triển bởi một nhóm sinh viên" | "do một nhóm sinh viên làm ra" |
| 14 | **"Điều này", "nó" và chuỗi "của"** | "Điều này khiến nó trở thành... của... của..." | Gộp câu, lược chủ ngữ, đổi cấu trúc |
| 15 | **Tránh "là" và "có"** | "đóng vai trò là", "sở hữu", "tọa lạc tại" | "là", "có", "ở" |

### D. Thổi phồng và mượn uy tín

| # | Mẫu | Trước | Sau |
|---|-----|-------|-----|
| 16 | **Từ AI dùng quá nhiều** | "không thể phủ nhận... đóng vai trò then chốt... kiến tạo... bức tranh" | Dùng từ thường |
| 17 | **Thổi phồng ý nghĩa** | "đánh dấu một bước ngoặt", "tương lai đầy hứa hẹn" | Giữ sự thật, bỏ ý nghĩa gán thêm |
| 18 | **Liên hệ mơ hồ** | "gắn liền với", "có mối liên hệ với" | Nêu đúng quan hệ nếu biết |
| 19 | **Đuôi câu "qua đó", "từ đó", "góp phần"** | "..., qua đó thể hiện khát vọng..." | Chỉ giữ điều nguồn ủng hộ |
| 20 | **Giọng quảng cáo** | "nằm ẩn mình", "thiên đường", "điểm đến không thể bỏ qua" | Nói nó là cái gì |
| 21 | **Mượn uy tín** | "Nhiều chuyên gia cho rằng...", "từng lên VTV, VnExpress..." | Nêu nguồn thật và nội dung, hoặc cắt |
| 22 | **Từ nhấn mạnh rỗng** (*yếu khi đứng một mình*) | "vô cùng quan trọng, hoàn toàn cần thiết" | Bỏ phần lớn |

### E. Giọng và xưng hô

| # | Mẫu | Trước | Sau |
|---|-----|-------|-----|
| 23 | **Xưng hô và giọng không khớp** | "Mình... Chúng tôi... Hãy... Chúng ta..." | Chọn một cách xưng hô và giữ nó |

### F. Định dạng theo công thức

| # | Mẫu | Trước | Sau |
|---|-----|-------|-----|
| 24 | **In đậm trang trí và chú thích tiếng Anh** | "**OKR (Objectives and Key Results - ...)**" | Bỏ in đậm, chú thích một lần khi cần |
| 25 | **Tiêu đề Viết Hoa Mọi Chữ, emoji và mũi tên** | "🚀 Chiến Lược Phát Triển", "👉 **Giai đoạn 1:**" | Viết hoa như câu thường, bỏ trang trí |
| 26 | **Ngoặc kép cong** (*yếu khi đứng một mình*) | `“...”` trộn với `"..."` | Giữ một kiểu nhất quán |

### G. Đồ thừa từ khung chat và bản nháp

| # | Mẫu | Trước | Sau |
|---|-----|-------|-----|
| 27 | **Dấu vết chatbot** | "Câu hỏi rất hay! ... Hy vọng thông tin này hữu ích!" | Bỏ phần bọc, giữ nội dung |
| 28 | **Đoạn kết "Tóm lại"** | "Tóm lại, ... Hãy bắt đầu ngay hôm nay!" | Cắt đoạn tóm tắt |
| 29 | **Giới hạn kiến thức và đoán mò** | "Hiện chưa có nhiều thông tin... nhiều khả năng..." | Nói nguồn không có gì, hoặc bỏ |
| 30 | **Tiêu đề lặp lại ở câu đầu** | "## Hiệu năng" + "Hiệu năng là yếu tố quan trọng." | Để tiêu đề làm việc của nó |
| 31 | **Viết về văn bản thay vì chủ đề** | "Bài viết này được chia thành ba phần", "được tổng hợp từ..." | Mô tả chủ đề |

### H. Viết cho sai người đọc

| # | Mẫu | Trước | Sau |
|---|-----|-------|-----|
| 32 | **Giải thích lại điều người đọc đã biết** | Câu trả lời đi hết phần chẩn đoán rồi mới tới quyết định | Đưa quyết định lên đầu |

## Ví dụ đầy đủ

**Trước (giọng AI):**
> Tháng Mười vừa rồi, mình đã có năm ngày không thể nào quên tại Đà Lạt — thành phố ngàn hoa thực sự đã đánh cắp trái tim mình. Ngay từ khoảnh khắc nhận phòng tại homestay xinh xắn nằm ẩn mình trên đồi thông, mình biết đây là một nơi vô cùng đặc biệt.
>
> Đà Lạt không chỉ là một điểm đến, mà là cả một trải nghiệm. Những con dốc quanh co tuy có phần thử thách, nhưng mỗi lần leo lên đều mang lại khung cảnh đẹp như tranh vẽ, khiến mọi nỗ lực đều trở nên xứng đáng.
>
> Và ẩm thực? Đơn giản là tuyệt vời. Bánh căn, bánh tráng nướng và sữa đậu nành nóng là những món ăn không thể bỏ qua, mang đậm hơi thở của phố núi. Đặc biệt, ly sữa đậu nành ở chợ đêm thực sự để lại dấu ấn sâu đậm trong mình.
>
> Tóm lại, Đà Lạt là một điểm đến tuyệt vời cho những ai muốn tìm về sự bình yên. Mình chắc chắn sẽ quay lại! ✨

**Sau:**
> Tháng Mười vừa rồi mình ở Đà Lạt năm ngày. Homestay nằm trên một đồi thông, từ đó đi đâu cũng phải leo dốc, chân mỏi nhừ, nhưng lên tới nơi thì cảnh đẹp thật.
>
> Ăn thì mình ăn bánh căn, bánh tráng nướng, tối nào cũng ra chợ đêm uống sữa đậu nành nóng. Ly sữa đậu nành là thứ mình nhớ nhất.
>
> Chắc chắn sẽ quay lại.

## Đóng góp

Rất mong cộng đồng góp thêm dấu hiệu và ví dụ. Đọc [AGENTS.md](AGENTS.md) trước khi sửa. Tóm tắt:

- Mở issue bằng mẫu **Dấu hiệu mới** kèm ví dụ thật và bản người viết. Phần lớn dấu hiệu mới gộp được vào mẫu có sẵn.
- Bản viết lại lỗi (còn sót dấu hiệu, đổi nghĩa, sửa quá tay, đổi sai giọng) thì mở issue **Lỗi viết lại**.
- Giữ `SKILL.md` và `README.md` khớp nhau. Chạy `python3 scripts/validate-package.py` trước khi gửi pull request.
- Ví dụ trong skill không được bịa sự thật. Bản "Sau" chỉ dùng thông tin có trong bản "Trước", hoặc ghi rõ là cần nguồn.

## Ghi công

- [Humanizer](https://github.com/blader/humanizer) của Siqi Chen (MIT): khung skill, cách làm và phần lớn các mẫu chung.
- [Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) của WikiProject AI Cleanup: nguồn gốc của bộ mẫu.

## Giấy phép

MIT. Xem [LICENSE](LICENSE).

---

## English

**Humanizer tiếng Việt** is a Vietnamese adaptation of [blader/humanizer](https://github.com/blader/humanizer). It rewrites AI-sounding Vietnamese text so it reads like a person wrote it, without changing what it says.

It keeps the original's method and most of its patterns, drops the English-only hyphenation rule, and adds tells specific to Vietnamese: translationese ("việc/sự" nominalization, "được... bởi" passives, "Điều này" openers, "một cách" adverbs), empty Sino-Vietnamese verbs ("tiến hành", "thực hiện"), stacked synonym pairs, inconsistent pronouns and register, Title Case headings, and the school-essay "Tóm lại" closing paragraph. It also knows that official documents and state-press prose used many of these forms long before AI, and edits them more gently.

Install with `npx skills add elderblack/humanizer-vietnam` or as a Claude Code plugin (see above), then call `/humanizer-vietnam`. MIT licensed.
