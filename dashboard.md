# OPERATING DASHBOARD — AI Trợ Lý Rà Soát Hợp Đồng Mua Bán Chung Cư

**Loại mô hình:** B2B · **Cập nhật:** 09/10/2026 · Lưu Mạnh Hưng – 2A202602942 · *Số liệu giả định, xem README*
**NORTH STAR:** Time-to-first-value (TTFV) — hiện tại 46 ngày — mục tiêu < 30 ngày

### Đèn báo sớm (Leading — nhìn hằng ngày/tuần)

| Đèn | Hiện | 🟢 / 🟡 / 🔴 | Nguồn | Báo trước cho |
|---|---|---|---|---|
| TTFV (ngày từ kick-off đến lô ≥20 HĐ thật được pháp chế xác nhận) | 46 ngày | 🟡 <30 / 30–60 / >60 | [TB] | POC→paid → CAC payback |
| Acceptance rate (flag AI được pháp chế giữ nguyên) | 71% (n=412 flag) | 🟡 ≥85 / 70–85 / <70 | [TB] | Usage depth |
| Cost/Job inference (đèn chi phí AI) | 38.000đ | 🟡 ≤33k / 33–41,25k / >41,25k | [MH] | Gross Margin |

### Đèn vận hành (Operating — nhìn hằng tuần/tháng)

| Đèn | Hiện | 🟢 / 🟡 / 🔴 | Nguồn | Báo trước cho |
|---|---|---|---|---|
| Usage depth (% seat ≥3 HĐ/tuần) | 38% | 🟡 ≥60 / 30–60 / <30 | [TB] | POC→paid, gia hạn năm 2 |
| POC → paid | 1/2 (n<5, chưa tô xanh) | 🟡 ≥50 / 35–50 / <35 | [BM] 27/08/2026 | CAC payback |
| Chi phí triển khai ÷ ACV | 29,5% | 🟡 ≤25 / 25–32,5 / >32,5 | [MH] | CAC payback |

### Đèn kết quả (Lagging — nhìn hằng quý)

| Đèn | Hiện | 🟢 / 🟡 / 🔴 | Nguồn |
|---|---|---|---|
| Gross Margin (trước chi phí triển khai) | 57,6% (theo giá niêm yết) | 🟢 ≥55 / 45–55 / <45 | [BM]+[MH] 27/08/2026 |
| CAC payback | 16,6 tháng (dự kiến) | 🟢 ≤18 / 18–24 / >24 | [MH]+[BM] 27/08/2026 |

### 5 luật quyết định (⏹ = luật dừng)

1. ⏹ NẾU TTFV >60 ngày TRÊN 2 khách gần nhất VÀ cả hai đã qua ≥60 ngày từ kick-off, THÌ dừng nhận POC rộng, thu hẹp mọi POC về 1 dự án + 1 mẫu HĐ + 1 nhóm pháp chế tới khi TTFV <30. KHÔNG THÌ không tuyển thêm sales, không mở thêm POC để lấp phễu.
2. ⏹ NẾU acceptance <70% TRONG 2 tuần liên tiếp VÀ mỗi tuần ≥200 flag, THÌ dừng ra tính năng mới 2 tuần, sửa 10 loại flag bị bác nhiều nhất rồi đo lại trên cùng bộ HĐ. KHÔNG THÌ không đổi sang model đắt hơn khi chưa biết lỗi ở loại flag nào.
3. ⏹ NẾU Cost/Job >41.250đ TRÊN 500 job gần nhất, THÌ dừng ký khách mới ở giá hiện tại; sprint tới chuyển phân loại điều khoản sang model nhỏ, bật cache, trần 3 lượt xử lý lại/HĐ. KHÔNG THÌ không tăng giá khách đang chạy, không cắt bước đối chiếu quy định pháp lý.
4. NẾU usage depth <30% SAU 60 ngày go-live ở một khách, THÌ cử 1 người vào khách 2 tuần gắn bước rà soát AI vào quy trình ký và đào tạo Sales. KHÔNG THÌ không bán thêm module cho khách đó, không giảm giá gia hạn.
5. ⏹ NẾU triển khai ÷ ACV >32,5% TRÊN 2 khách liên tiếp, THÌ dừng nhận triển khai tuỳ biến, 4 tuần chuẩn hoá connector CRM/DMS và playbook thành template, báo giá phí triển khai riêng. KHÔNG THÌ không nhận khách mới cùng mức giá, không nhận yêu cầu sửa riêng.

### Cổng gác 90 ngày

| Ngày | Metric (1) | Ngưỡng qua cổng | Bằng chứng | Nếu trượt |
|---|---|---|---|---|
| 30 (08/11/2026) — cổng học | Số HĐ thật có nhãn accept/reject của pháp chế | ≥150 HĐ (≈1.800 flag, sai số ±2,3 điểm %) trên ≥2 chủ đầu tư | File nhãn đã ẩn danh + Evidence Pack v1 | FIX 1 lần nếu biết nguyên nhân (30 ngày); khách không cấp dữ liệu → PIVOT sang khách khác |
| 60 (08/12/2026) | TTFV của 2 khách pilot gần nhất | Cả hai < 30 ngày | Sheet kick-off + biên bản xác nhận lô ≥20 HĐ của pháp chế | FIX nếu chưa FIX; đã FIX ở ngày 30 cho cùng vấn đề → PIVOT (đổi phân khúc/value metric) |
| 90 (07/01/2027) | Số chủ đầu tư ký trả tiền hoặc LOI có giá | ≥1, ACV ≥1,16 tỷ đ (sàn payback 18 tháng) | Hợp đồng/LOI (ẩn danh) + Pilot Report có số | KILL nếu đã FIX 1 lần; chưa FIX → FIX 1 lần rồi xét lại ở ngày 120 |

**KILL CRITERIA:** Đến 07/01/2027, nếu chưa có chủ đầu tư nào ký trả tiền hoặc LOI có giá ACV ≥1,16 tỷ đ và TTFV vẫn >60 ngày sau 1 lần FIX → dừng dòng sản phẩm cho chủ đầu tư (runway thật còn ~2,6 tháng).

**CHƯA ĐO ĐƯỢC:** (1) **NRR** — cần ≥12 tháng sau hợp đồng trả tiền đầu tiên, dự kiến có số quý 1/2028. (2) **Tỷ lệ bỏ sót điều khoản rủi ro (recall)** — acceptance chỉ đo flag AI đưa ra, không đo flag AI bỏ sót; cần luật sư gán nhãn ≥100 HĐ gài sẵn lỗi, dự kiến 08/11/2026. (3) **% deal chết ở security/procurement** và **sales cycle** — mới có 2 deal, cần ≥10 deal đóng, dự kiến quý 2/2027. (4) Gross Margin và payback hiện tính theo giá niêm yết, chưa có doanh thu thật.
