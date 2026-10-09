# Worksheet — AI Trợ Lý Rà Soát Hợp Đồng Mua Bán Chung Cư

Họ tên: Lưu Mạnh Hưng · MSSV: 2A202602942 · Ngày làm: 09/10/2026

> ⚠️ **Số liệu giả định.** Sản phẩm chưa có số thật nên mọi số về mô hình tài chính, Cost/Job và pilot ("Chủ đầu tư A", "Chủ đầu tư B") đều là giả định để luyện bài. Benchmark [BM] lấy từ HANDBOOK §8, kiểm tra ngày 27/08/2026.

## Trạm 1 — Loại mô hình

**Câu chốt loại:** Chúng tôi là **B2B** vì tiền đến từ chủ đầu tư bất động sản (Chủ đầu tư A), người dùng là chính nhân viên Sales và Pháp chế của họ chứ không phải người mua căn hộ, và chúng tôi không chạm được người mua — sản phẩm chạy hoàn toàn trong quy trình nội bộ của khách. (Không phải B2B2C: người mua căn hộ không phải là khách hàng cuối của chúng tôi.)

**Bảng đèn §3.2 B2B** (đủ 11 đèn trong bảng):

| Đèn | ✅ / 🔧 / ❌ | Số nằm ở đâu / cần gì để đo |
|---|---|---|
| Time-to-first-value (TTFV) | ✅ | Sheet CS theo dõi ngày kick-off + biên bản pháp chế xác nhận lô hợp đồng thật. Có 2 pilot (A, B) |
| Pipeline coverage | 🔧 | CRM chưa định nghĩa stage "đủ điều kiện". Cần chốt định nghĩa và cập nhật giá trị cơ hội, 2 tuần |
| % deal chết ở security/procurement | 🔧 | Thêm trường "lý do mất deal" vào CRM, 2 tuần. Còn ít deal nên cần ≥10 deal đóng mới đọc được |
| POC → paid | ✅ | CRM: 2 pilot, 1 đã ký, 1 đang đàm phán |
| Sales cycle | 🔧 | CRM có timestamp tạo cơ hội. Có số khi ≥3 deal đóng (dự kiến Q1/2027) |
| Usage depth | ✅ | Event analytics: số HĐ rà soát theo seat theo tuần |
| Chi phí triển khai ÷ ACV | 🔧 | Hiện ước lượng từ timesheet thủ công. Cần log giờ công theo task theo khách, 2 tuần |
| Tập trung doanh thu | 🔧 | Billing. Chưa có doanh thu trả tiền nên chưa tính được, có số khi ≥2 khách trả tiền |
| NRR | ❌ | Cần ≥12 tháng kể từ hợp đồng trả tiền đầu tiên. Chưa biết cách đo sớm hơn |
| Gross Margin | ✅ | Log token theo job (inference) + phân bổ hosting/support/QA. Hiện tính theo giá niêm yết dự kiến, chưa có doanh thu thật |
| CAC payback | 🔧 | Cần chuẩn hoá cách phân bổ chi phí sales/marketing cho từng khách, 2 tuần |

## Trạm 2 — Thẻ đèn

**North Star:** Time-to-first-value (TTFV) — hiện tại 46 ngày (A 41, B 51) — mục tiêu < 30 ngày

Lý do chọn: đây là đèn bật trước của B2B (HANDBOOK §2.5). Pilot nào không có lô hợp đồng thật được pháp chế dùng trong 30 ngày thì gần như không chuyển thành hợp đồng trả tiền.

| # | Tầng (L/O/G) | Đèn | Định nghĩa (đếm gì · **không** đếm gì) | Công thức | Nhịp · ai lấy số | Báo trước cho |
|---|---|---|---|---|---|---|
| 1 | L | **TTFV** | Số ngày từ kick-off POC (cấp tài khoản) đến ngày pháp chế của khách xác nhận bằng văn bản đã rà xong **≥1 lô ≥20 hợp đồng thật** và dùng kết quả. **Không** đếm: demo trên hợp đồng mẫu, cài đặt xong, đào tạo xong | Ngày xác nhận lô đầu − ngày kick-off | Mỗi khách · CS lead | #5 POC→paid, sau đó #8 CAC payback |
| 2 | L | **Acceptance rate** (tỷ lệ pháp chế chấp nhận) | % flag do AI đưa ra mà pháp chế **giữ nguyên hoặc chỉ sửa câu chữ**. **Không** đếm: flag trên hợp đồng test, flag chưa được ai xem, flag pháp chế bỏ qua không gán nhãn | Flag được chấp nhận ÷ flag đã được pháp chế gán nhãn (chỉ tính tuần ≥200 flag) | Tuần · PM | #4 Usage depth |
| 3 | L | **Cost/Job** (đèn chi phí AI) | Chi phí inference trung bình của một hợp đồng rà xong (token vào + ra + lượt xử lý lại + embedding). **Không** đếm: hosting, support, nhân sự | Tổng chi phí API trong kỳ ÷ số hợp đồng rà xong, 500 job gần nhất | Tuần · Eng lead (từ log) | #7 Gross Margin |
| 4 | O | **Usage depth** | % seat đã go-live ≥30 ngày mà có **≥3 hợp đồng rà soát trong tuần**. **Không** đếm: seat admin/IT, seat test, đăng nhập mà không rà hợp đồng | Seat đạt ≥3 HĐ/tuần ÷ seat đã go-live ≥30 ngày | Tuần · CS lead | #5 POC→paid (trong POC) và gia hạn năm 2 |
| 5 | O | **POC → paid** | % POC kết thúc có hợp đồng trả tiền hoặc LOI có giá. **Không** đếm: POC đang chạy, gia hạn POC miễn phí | POC chuyển trả tiền ÷ POC đã kết thúc | Quý · Founder | #8 CAC payback |
| 6 | O | **Chi phí triển khai ÷ ACV** | Giờ công triển khai × đơn giá + chi phí tích hợp CRM/DMS + chuẩn hoá mẫu hợp đồng, tính theo khách. **Không** đếm: chi phí bán hàng (đã nằm trong CAC) | (Giờ công × đơn giá + tích hợp + chuẩn hoá) ÷ ACV | Mỗi khách · CS lead | #8 CAC payback |
| 7 | G | **Gross Margin** | (Doanh thu − inference − hosting/support/QA) ÷ doanh thu, **trước** chi phí triển khai một lần | Công thức Day 24 | Quý · Founder | — (bảng điểm) |
| 8 | G | **CAC payback** | Số tháng để lãi gộp hoàn lại (CAC + chi phí triển khai) | (CAC + triển khai) ÷ (MRR × GM) | Quý · Founder | — (bảng điểm) |

Đèn chi phí AI là đèn số **3 (Cost/Job)**: nó đổi theo tuần và báo trước Gross Margin (đèn 7) cả quý.

Cơ cấu tầng: Leading 3 · Operating 3 · Lagging 2 (25% lagging, dưới ngưỡng 50%).

## Trạm 3 — Ngưỡng

| # | Đèn | 🟢 | 🟡 | 🔴 | Nguồn [BM]/[MH]/[TB] | Lý do (1 câu) · ngày kiểm tra nếu [BM] |
|---|---|---|---|---|---|---|
| 1 | TTFV | < 30 ngày | 30–60 | > 60 | [TB] | Chưa có baseline ngành cho AI pháp lý; 30 ngày ≈ một lô hợp đồng của một đợt mở bán, còn > 60 ngày là quá nửa POC 90 ngày nên khách chưa thấy giá trị trước lúc quyết định. Baseline hiện 46 ngày; đo 2 chu kỳ rồi chốt lại, dự kiến 08/12/2026 |
| 2 | Acceptance rate | ≥ 85% | 70–85% | < 70% | [TB] | Chưa có chuẩn ngành; baseline hiện 71% (412 flag, 34 HĐ, 2 pilot). 85% nghĩa là pháp chế chỉ sửa ≤ 1/7 flag. Chốt lại sau 2 chu kỳ, dự kiến 08/12/2026 |
| 3 | Cost/Job | ≤ 33.000đ | 33.000–41.250đ | > 41.250đ | [MH] #1 | Trần 41.250đ suy ra từ GM sàn 55%; 🟢 đặt ở 80% mức trần để còn đệm cho hợp đồng dài |
| 4 | Usage depth | ≥ 60% | 30–60% | < 30% | [TB] | Mỗi đợt mở bán sinh ra lô hợp đồng nên pháp chế phải dùng hằng tuần; baseline hiện 38%, chốt lại sau 2 chu kỳ, dự kiến 08/12/2026 |
| 5 | POC → paid | ≥ 50% | 35–50% | < 35% | [BM] | ICONIQ *State of Go-to-Market 2026*: POC → paid ~50% (2026), ~36% (2025); kiểm tra 27/08/2026. Chỉ tô 🟢 khi đã có ≥5 POC kết thúc, vì mẫu nhỏ dễ nhiễu |
| 6 | Chi phí triển khai ÷ ACV | ≤ 25% | 25–32,5% | > 32,5% | [MH] #2 | Trần 32,5% là phần ngân sách còn lại sau CAC để payback ≤ 18 tháng; 🟢 chừa đệm 90 triệu đồng ≈ 1,6 tháng lãi gộp |
| 7 | Gross Margin | ≥ 55% | 45–55% | < 45% | [BM] + [MH] #1 | ICONIQ *State of AI 2026*: AI-native 45% (2025) → 53% (2026P); kiểm tra 27/08/2026. Nâng 🟢 lên 55% vì phép tính Cost/Job dùng 55% làm sàn |
| 8 | CAC payback | ≤ 18 tháng | 18–24 | > 24 | [MH] #3 + [BM] | Enterprise < 24 tháng (Bessemer, David Skok; kiểm tra 27/08/2026). Đặt 🟢 chặt hơn ở 18 tháng vì runway chỉ 10 tháng (xem [MH] #4) |

### Phụ lục [MH] — phép tính (3 ngưỡng + 1 ràng buộc runway)

**[MH] 1 — Cost/Job**

```
Đầu vào (giả định): ACV = 1,2 tỷ đ/năm = 100.000.000đ/tháng · 800 hợp đồng/tháng/khách
                    chi phí ngoài inference = 12% doanh thu · GM sàn = 55%
Phép tính: doanh thu/job            = 100.000.000 ÷ 800        = 125.000đ
           COGS tối đa/job          = 125.000 × (1 − 55%)      = 56.250đ
           chi phí ngoài inference  = 125.000 × 12%            = 15.000đ
           inference tối đa         = 56.250 − 15.000          = 41.250đ
           🟢 = 80% mức tối đa      = 41.250 × 0,8             = 33.000đ
Kết quả → 🟢 ≤ 33.000đ · 🟡 33.000–41.250đ · 🔴 > 41.250đ
Hiện 38.000đ → GM = (125.000 − 38.000 − 15.000) ÷ 125.000 = 57,6% (🟡 ở Cost/Job, 🟢 ở GM)
```

**[MH] 2 — Chi phí triển khai ÷ ACV**

```
Đầu vào: payback tối đa 18 tháng · GM 55% · CAC/khách = 600.000.000đ · ACV = 1.200.000.000đ
Phép tính: lãi gộp/tháng            = 100.000.000 × 55%        = 55.000.000đ
           ngân sách CAC + triển khai = 55.000.000 × 18        = 990.000.000đ
           triển khai tối đa        = 990.000.000 − 600.000.000 = 390.000.000đ
           tỷ lệ tối đa             = 390 ÷ 1.200              = 32,5% ACV
           🟢 = 300.000.000đ (25%), chừa đệm 90.000.000đ ≈ 1,6 tháng lãi gộp
Kết quả → 🟢 ≤ 25% · 🟡 25–32,5% · 🔴 > 32,5%
Hiện: 360 giờ × 400.000đ = 144.000.000đ + tích hợp CRM/DMS 120.000.000đ
      + chuẩn hoá 40 mẫu hợp đồng và playbook 90.000.000đ = 354.000.000đ → 29,5% (🟡)
```

**[MH] 3 — CAC payback và ACV sàn**

```
Đầu vào: CAC 600.000.000đ + triển khai 354.000.000đ = 954.000.000đ · GM hiện 57,6% · MRR 100.000.000đ
Phép tính: payback hiện = 954 ÷ (100 × 57,6%) = 954 ÷ 57,6 = 16,6 tháng  → 🟢 (≤ 18)
           ACV sàn để payback ≤ 18 tháng:
             lãi gộp/tháng cần = 954 ÷ 18 = 53,0 triệu đ
             MRR cần = 53,0 ÷ 55% = 96,4 triệu đ/tháng → ACV ≥ 96,4 × 12 = 1.157 triệu ≈ 1,16 tỷ đ
Kết quả → 🟢 ≤ 18 tháng · 🟡 18–24 · 🔴 > 24; hợp đồng đầu tiên phải có ACV ≥ 1,16 tỷ đ
```

**[MH] 4 — Runway so với chu kỳ bán (dùng cho kill criteria)**

```
Đầu vào: runway = 10 tháng (giả định) · chu kỳ bán ~19 tuần ([BM] ICONIQ GTM 2026, kiểm tra 27/08/2026)
Phép tính: 19 tuần × 7 ÷ 30,4 = 4,4 tháng → thời gian thật sự có để chứng minh = 10 − 4,4 = 5,6 tháng
           90 ngày = 3 tháng → sau cổng ngày 90 chỉ còn ~2,6 tháng
Kết quả → cổng ngày 90 là mốc cuối để quyết định KILL; không thể để FIX lần hai
```

## Trạm 4 — 5 luật quyết định

⏹ = luật dừng (có 4 luật).

1. ⏹ **NẾU** TTFV > 60 ngày **TRÊN** 2 khách gần nhất **VÀ** cả hai đã qua ≥60 ngày kể từ kick-off **THÌ** dừng nhận POC rộng; thu hẹp mọi POC còn lại về 1 dự án căn hộ + 1 mẫu hợp đồng + 1 nhóm pháp chế cho tới khi TTFV < 30 ngày **KHÔNG THÌ** không tuyển thêm sales và không mở thêm POC để lấp phễu.
2. ⏹ **NẾU** acceptance rate < 70% **TRONG** 2 tuần liên tiếp **VÀ** mỗi tuần ≥200 flag đã gán nhãn **THÌ** dừng phát hành tính năng mới 2 tuần; lấy 10 loại flag bị bác nhiều nhất, sửa prompt/quy tắc, thêm vào bộ eval rồi đo lại trên cùng bộ hợp đồng **KHÔNG THÌ** không đổi sang model đắt hơn khi chưa biết lỗi nằm ở loại flag nào (Cost/Job sẽ vượt trần).
3. ⏹ **NẾU** Cost/Job trung bình > 41.250đ **TRÊN** 500 job gần nhất **THÌ** dừng ký khách mới ở mức giá hiện tại; trong sprint tới chuyển bước phân loại điều khoản sang model nhỏ, bật cache và đặt trần 3 lượt xử lý lại mỗi hợp đồng **KHÔNG THÌ** không tăng giá với khách đang chạy và không cắt bước đối chiếu quy định pháp lý để giảm chi phí.
4. **NẾU** usage depth < 30% **SAU** 60 ngày kể từ go-live ở một khách **THÌ** cử 1 người vào khách trong 2 tuần để gắn bước rà soát AI vào quy trình ký (checklist bắt buộc trước khi pháp chế duyệt) và đào tạo nhóm Sales **KHÔNG THÌ** không bán thêm dự án/module cho khách đó và không giảm giá gia hạn.
5. ⏹ **NẾU** chi phí triển khai ÷ ACV > 32,5% **TRÊN** 2 khách liên tiếp **THÌ** dừng nhận triển khai tuỳ biến; trong 4 tuần chuẩn hoá connector CRM/DMS và playbook điều khoản thành template, đồng thời báo giá phí triển khai riêng **KHÔNG THÌ** không nhận khách mới ở cùng mức giá và không nhận yêu cầu sửa riêng cho khách đó.
