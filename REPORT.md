# Báo cáo LAB 17 — Data Pipeline Engineering

**Họ tên:** Nguyễn Thành An - 2A202601017  **Lớp:** K3-Track 2  **Ngày:** 

---

## 0 · Kết quả `make verify`

<details>
<summary>Lần 1</summary>

```
(.venv) PS E:\AI\Lab\Phase 2\Track2-Day17-K3-01017-NguyenThanhAn> make verify 

  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  LAB 17 · make verify
  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  run 1/3 … 61.4s
  run 2/3 … 57.1s
  run 3/3 … 52.3s

  BẢNG                  ỔN ĐỊNH          SỐ HÀNG     KỲ VỌNG   GHI CHÚ
  ──────────────────────────────────────────────────────────────────────────
  gold_training_set     ✓ ok              12,480      12,480   ✓
  gold_feature_daily    ✓ ok               8,645       9,100   ✗ thiếu 455 hàng
  gold_doc_chunks       ✓ ok              31,200      31,200   ✓
  quarantine_tickets    ✓ ok                   0         312   ✗ thiếu 312 hàng

  CHECKSUM từng lượt
  ──────────────────────────────────────────────────────────────────────────
  gold_training_set     8622572a97    8622572a97    8622572a97   ✓
  gold_feature_daily    4eee63cd82    4eee63cd82    4eee63cd82   ✓
  gold_doc_chunks       92d8e50131    92d8e50131    92d8e50131   ✓
  quarantine_tickets    empty         empty         empty        ✓

  KIỂM TRA KHÁC
  ──────────────────────────────────────────────────────────────────────────
  dbt test                                    ✓ 9/9 pass
  silver_tickets.priority ∈ 1..4, không NULL  ✗ 6,606 hàng sai
  quarantine_tickets đúng số bản ghi lỗi      ✗ 0 / 312
  gold_training_set: 1 hàng / 1 ticket        ✓ không lặp
  dashboard rows scanned                      ✗ 5,000,000 → 5,000,000 (1.0×, cần ≥ 10×)
    số file parquet                           ✗ 5,000 → 5,000
    kết quả truy vấn không đổi                ✓
  DAG: catchup / max_active_runs              ✓ False / 1

  TỔNG KẾT
  ──────────────────────────────────────────────────────────────────────────
  ✓  1 · gold_training_set idempotent & đúng số hàng
  ✗  2 · gold_feature_daily đủ hàng (dữ liệu về muộn)
  ✗  3 · contract + quarantine + dbt test
  ✓  4 · gold_doc_chunks vẫn ổn định (đối chứng)
  ──────────────────────────────────────────────────────────────────────────
  2/4 tiêu chí đạt
```

</details>

<details>
<summary>Lần 2</summary>

```

(.venv) PS E:\AI\Lab\Phase 2\Track2-Day17-K3-01017-NguyenThanhAn> make verify  

  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  LAB 17 · make verify
  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  run 1/3 … 62.1s
  run 2/3 … 58.0s
  run 3/3 … 54.8s

  BẢNG                  ỔN ĐỊNH          SỐ HÀNG     KỲ VỌNG   GHI CHÚ
  ──────────────────────────────────────────────────────────────────────────
  gold_training_set     ✓ ok              12,480      12,480   ✓
  gold_feature_daily    ✓ ok               9,100       9,100   ✓
  gold_doc_chunks       ✓ ok              31,200      31,200   ✓
  quarantine_tickets    ✓ ok                   0         312   ✗ thiếu 312 hàng

  CHECKSUM từng lượt
  ──────────────────────────────────────────────────────────────────────────
  gold_training_set     8622572a97    8622572a97    8622572a97   ✓
  gold_feature_daily    3db448685c    3db448685c    3db448685c   ✓
  gold_doc_chunks       92d8e50131    92d8e50131    92d8e50131   ✓
  quarantine_tickets    empty         empty         empty        ✓

  KIỂM TRA KHÁC
  ──────────────────────────────────────────────────────────────────────────
  dbt test                                    ✓ 9/9 pass
  silver_tickets.priority ∈ 1..4, không NULL  ✗ 6,606 hàng sai
  quarantine_tickets đúng số bản ghi lỗi      ✗ 0 / 312
  gold_training_set: 1 hàng / 1 ticket        ✓ không lặp
  dashboard rows scanned                      ✗ 5,000,000 → 5,000,000 (1.0×, cần ≥ 10×)
    số file parquet                           ✗ 5,000 → 5,000
    kết quả truy vấn không đổi                ✓
  DAG: catchup / max_active_runs              ✓ False / 1

  TỔNG KẾT
  ──────────────────────────────────────────────────────────────────────────
  ✓  1 · gold_training_set idempotent & đúng số hàng
  ✓  2 · gold_feature_daily đủ hàng (dữ liệu về muộn)
  ✗  3 · contract + quarantine + dbt test
  ✓  4 · gold_doc_chunks vẫn ổn định (đối chứng)
  ──────────────────────────────────────────────────────────────────────────
  3/4 tiêu chí đạt
```

</details>

<details>
<summary>Lần 3</summary>

```
(.venv) PS E:\AI\Lab\Phase 2\Track2-Day17-K3-01017-NguyenThanhAn> make verify 

  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  LAB 17 · make verify
  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  run 1/3 … 50.0s
  run 2/3 … 49.8s
  run 3/3 … 47.4s

  BẢNG                  ỔN ĐỊNH          SỐ HÀNG     KỲ VỌNG   GHI CHÚ
  ──────────────────────────────────────────────────────────────────────────
  gold_training_set     ✓ ok              12,480      12,480   ✓
  gold_feature_daily    ✓ ok               9,100       9,100   ✓
  gold_doc_chunks       ✓ ok              31,200      31,200   ✓
  quarantine_tickets    ✓ ok                 312         312   ✓

  CHECKSUM từng lượt
  ──────────────────────────────────────────────────────────────────────────
  gold_training_set     8dd7c98653    8dd7c98653    8dd7c98653   ✓
  gold_feature_daily    3db448685c    3db448685c    3db448685c   ✓
  gold_doc_chunks       92d8e50131    92d8e50131    92d8e50131   ✓
  quarantine_tickets    ebb89036fb    ebb89036fb    ebb89036fb   ✓

  KIỂM TRA KHÁC
  ──────────────────────────────────────────────────────────────────────────
  dbt test                                    ✓ 11/11 pass
  silver_tickets.priority ∈ 1..4, không NULL  ✓ sạch
  quarantine_tickets đúng số bản ghi lỗi      ✓ 312 / 312
  gold_training_set: 1 hàng / 1 ticket        ✓ không lặp
  dashboard rows scanned                      ✗ 5,000,000 → 5,000,000 (1.0×, cần ≥ 10×)
    số file parquet                           ✗ 5,000 → 5,000
    kết quả truy vấn không đổi                ✓
  DAG: catchup / max_active_runs              ✓ False / 1

  TỔNG KẾT
  ──────────────────────────────────────────────────────────────────────────
  ✓  1 · gold_training_set idempotent & đúng số hàng
  ✓  2 · gold_feature_daily đủ hàng (dữ liệu về muộn)
  ✓  3 · contract + quarantine + dbt test
  ✓  4 · gold_doc_chunks vẫn ổn định (đối chứng)
  ──────────────────────────────────────────────────────────────────────────
  4/4 tiêu chí đạt
```

</details>

---

Tổng kết: **4/4 tiêu chí đạt**

## 1 · Kích thước bảng training tăng sau mỗi lần chạy

| | |
|---|---|
| **Triệu chứng** | Sau mỗi lần chạy pipeline, `count(*)` của `gold_training_set` tăng thêm xấp xỉ số row của lần trước. Chạy lần 1 được 13.790 row, chạy lần 2 được 26.270 row - gần gấp đôi. |
| **Nguyên nhân** | `gold_training_set` là incremental model nhưng không khai báo `unique_key` => dbt không biết dòng nào là "cùng ticket". Khi thiếu `unique_key`, dbt sinh ra `INSERT` không điều kiện (`append`). Mỗi lần pipeline chạy lại cùng partition ngày, toàn bộ row trong window đó bị ghi thêm vào bảng thay vì ghi đè - khiến số row tăng tuyến tính theo số lần chạy. |
| **Cách khắc phục** | **`dbt/models/gold/gold_training_set.sql`**: thêm `unique_key = 'ticket_id'` và `incremental_strategy = 'merge'` vào `config()`. dbt sẽ sinh ra câu `MERGE` - UPDATE nếu `ticket_id` đã tồn tại, INSERT nếu mới. Chọn `merge` (không phải `delete+insert`) vì source CDC có `op='u'`: một ticket được tạo ngày D1 và sửa ngày D2 có hai bản ghi CDC với `_ingested_at` khác nhau; `delete+insert` theo partition ngày sẽ bỏ sót bản ghi update nằm ở partition khác. **`dags/ai_training_pipeline.py`**: đặt `catchup=False` và `max_active_runs=1` để giảm tần suất kích hoạt lỗi (không phải root cause, nhưng bắt buộc theo rubric). |
| **Bằng chứng** | trước fix: lần 1 -> 13.790 hàng, lần 2 -> 26.270 hàng (≈ ×2) · sau fix: 12.480 hàng · checksum 3 lượt: `8dd7c98653` (ổn định) |

---

## 2 · Bảng đặc trưng theo ngày thiếu hàng ở các ngày quá khứ

| | |
|---|---|
| **Triệu chứng** | `gold_feature_daily` chỉ có 8.645 / 9.100 hàng kỳ vọng. Các cặp `(event_date, customer_id)` bị thiếu tập trung ở các ngày cũ, không phải ngày mới. |
| **P99 độ trễ đo được** | **2.73 ngày** (P50 = 0.13 ngày, P95 = 1.81 ngày, max = 2.94 ngày, ~5% bản ghi tới muộn hơn 1 ngày) |
| **Lookback đã chọn** | 3 ngày - làm tròn lên từ P99 = 2.73 ngày để bao phủ 99% trường hợp tới muộn |
| **Nguyên nhân** | Điều kiện lọc incremental dùng `event_date > max(event_date)` - chỉ xử lý những ngày **mới hơn** ngày lớn nhất đã có trong target. Một event xảy ra ngày 08-12 nhưng `_ingested_at = 08-15`: tại lượt chạy ngày 08-15, `max(event_date)` trong target là 08-14, nên `08-12 > 08-14` = FALSE - event bị bỏ qua vĩnh viễn. Các ngày tiếp theo `max` tiếp tục tăng nên event đó không bao giờ lọt qua điều kiện. |
| **Cách khắc phục** | **`dbt/models/gold/gold_feature_daily.sql`**: (1) đổi điều kiện lọc thành `event_date >= max(event_date) - interval 3 day` để tính lại 3 ngày gần nhất; (2) thêm `unique_key = ['event_date', 'customer_id']` và `incremental_strategy = 'merge'` vào `config()` - vì window rộng hơn khiến cùng một cặp được tính lại nhiều lần, nếu không có merge thì lại tái tạo lỗi cộng dồn của nhiệm vụ 1. |
| **Bằng chứng** | trước: 8.645 hàng · sau: 9.100 hàng · checksum 3 lượt: `3db448685c` (ổn định) |

Vì sao chọn P99 làm căn cứ thay vì `max`? Chi phí của mỗi lựa chọn là gì?

> P99 (2.73 ngày) bao phủ 99% trường hợp dữ liệu tới muộn với lookback 3 ngày. Dùng `max` (2.94 ngày) chỉ bảo vệ thêm 1% còn lại nhưng phải trả giá ở **mọi lượt chạy sau này**: mỗi ngày lùi thêm nghĩa là pipeline phải tính lại thêm 650 cặp (customer) × 1 ngày = 650 row thêm, nhân với tần suất hàng ngày trong nhiều năm vận hành. Chi phí của max là chi phí tái diễn vô thời hạn, không phải một lần.

---

## 3 · Kiểu dữ liệu cột priority thay đổi giữa chu kỳ

| | |
|---|---|
| **Triệu chứng** | Từ 2026-08-10, `silver_tickets.priority` có 6.606 hàng NULL hoặc ngoài khoảng 1..4. `quarantine_tickets` rỗng (0 hàng). Phân bố `priority_raw` trong source có cả nhãn chữ (`urgent`, `high`, `medium`, `low`) lẫn giá trị sai (`P1`, `0`, `-1`, `unknown`). |
| **Nguyên nhân** | Macro `normalize_priority` dùng `try_cast(priority_raw as integer)`: hàm này biến nhãn chữ (`urgent`...) thành NULL - vứt bỏ dữ liệu hợp lệ - đồng thời lại chấp nhận `'0'`, `'5'`, `'-1'` vì chúng cast được sang integer dù nằm ngoài contract. Từ ngày 08-10, team backend đổi format ghi từ số sang nhãn chữ; `try_cast` không hiểu nhãn chữ nên toàn bộ ticket mới đều ra NULL ở cột priority. |
| **Ba nhóm giá trị `priority` và cách xử lý từng nhóm** | **Nhóm 1** - `'1' '2' '3' '4'`: số hợp lệ theo contract cũ -> giữ nguyên (cast integer). **Nhóm 2** - `'urgent' 'high' 'medium' 'low'`: schema evolution, source đổi cách biểu diễn nhưng ý nghĩa không đổi -> map về số (urgent=1, high=2, medium=3, low=4). **Nhóm 3** - `'P1' 'unknown' '0' '5' '-1' '' NULL`: dữ liệu hỏng thật -> trả về NULL để quarantine bắt. |
| **Cách khắc phục** | **(a) `dbt/macros/normalize_priority.sql`**: thay `try_cast` bằng CASE xử lý đủ 3 nhóm. **(b) `dbt/models/silver/silver_tickets.sql`**: tách thành CTE `normalized -> valid (lọc NULL) -> ranked` - lọc bản ghi hỏng trước khi xếp hạng để ticket vẫn giữ được bản ghi hợp lệ cũ. **(c) `dbt/models/silver/quarantine_tickets.sql`**: thay `where false` bằng `where normalize_priority(priority_raw) is null`. **(d) `dbt/models/silver/schema.yml`**: bật `enforced: true`, thêm test `not_null` và `accepted_values: [1,2,3,4]` trên cột `priority`. |
| **Bằng chứng** | `quarantine_tickets` = 312 hàng · `dbt test` 11/11 pass |

Câu hỏi thiết kế: nên chặn ở tầng Bronze hay Silver? Vì sao **không** để
pipeline dừng khi gặp bản ghi lỗi?

> Nên chặn ở Silver, không phải Bronze. Bronze là nơi lưu dữ liệu thô nguyên vẹn - nếu Bronze từ chối row lỗi, dữ liệu đó biến mất khỏi hệ thống vĩnh viễn; khi cần điều tra nguồn gốc sự cố (tại sao source gửi `'P1'`?) hoặc cần replay sau khi fix, không còn gì để trace lại. Silver là nơi áp dụng contract: giữ nguyên ở Bronze, lọc ở Silver, đưa bản ghi lỗi vào quarantine để người trực xử lý.
>
> 312 bản ghi lỗi (<0.3% tổng CDC) không có quyền chặn 130.000+ event và 31.200 chunk hoàn toàn bình thường đang chờ phục vụ người dùng. Dừng toàn bộ pipeline vì một số nhỏ bản ghi lỗi là trade-off sai: thiệt hại cho 99.7% dữ liệu tốt lớn hơn nhiều so với việc để 312 bản ghi chờ trong quarantine.

---

## 4 · *(mở rộng, không bắt buộc)* Bài trong EXTRA.md

### Bài A
<details>
<summary>Scan trước sửa</summary>

```
(.venv) PS E:\AI\Lab\Phase 2\Track2-Day17-K3-01017-NguyenThanhAn> make explain

  queries/dashboard.sql
  --------------------------------------------------------------
                              TRƯỚC        HIỆN TẠI      MỤC TIÊU
  rows scanned           5,000,000       5,000,000     ≤ 500,000   ✗
  rows on disk             130,683         130,683   (tham khảo)
  files                      5,000           5,000        ít hơn   ✗
  result hash         4379e4c5d9f3    4379e4c5d9f3     không đổi   ✓
  thời gian (ms)                 —         3,114.0   (tham khảo)

  => giảm 1.0× (cần ≥ 10×)

  kết quả truy vấn (1 hàng):
    ('ACME', 3500, 3068, 2521.1, 4691, 262, 7764750)
```

</details>

| | |
|---|---|
| **Bài đã làm** | Bài A |
| **Nguyên nhân** | Dataset gồm 5.000 file paarquet nhỏ (~26 hàng/file), không partition. DuckDB đọc tối thiểu ~1.000 hàng/file nên phải scan 5.000.000 hàng dù dữ liệu thực chỉ có 130.683. Ngoài ra filter `strftime(event_time, '%Y-%m-%d') = '...'` bọc cột trong function call -> engine không so được với min/max của row group và không pruning được theo directory partition. |
| **Cách khắc phục** | (1) Gom 5.000 file thành dataset mới partition theo `event_date` (14 file, 1 file/ngày). Sắp xếp `ORDER BY event_date, customer_name, event_time` để row group statistics của customer có ích. (2) Sửa `dashboard.sql` trỏ vào dataset mới với `hive_partitioning=true` và viết lại filter thành `event_date = '2026-08-09'` (predicate sargable) - DuckDB đọc tên thư mục và bỏ qua 13 thư mục còn lại mà không mở file. |
| **Bằng chứng** | rows scanned: 5.000.000 -> 136.948 (giảm 36.5×, cần ≥10×) · files: 5.000 -> 14 · result hash: `4379e4c5d9f3` (không đổi) |

<details>
<summary>Scan A sau sửa</summary>

```
(.venv) PS E:\AI\Lab\Phase 2\Track2-Day17-K3-01017-NguyenThanhAn> make compact  
  nguồn : E:\AI\Lab\Phase 2\Track2-Day17-K3-01017-NguyenThanhAn\data\gold_events  (5,000 file)
  đích   : E:\AI\Lab\Phase 2\Track2-Day17-K3-01017-NguyenThanhAn\data\gold_events_v2  (14 file)
  hàng   : 130,683 → 130,683  ✓
(.venv) PS E:\AI\Lab\Phase 2\Track2-Day17-K3-01017-NguyenThanhAn> make explain 

  queries/dashboard.sql
  --------------------------------------------------------------
                             TRƯỚC        HIỆN TẠI      MỤC TIÊU
  rows scanned           5,000,000         136,948     ≤ 500,000   ✓
  rows on disk             130,683         130,683   (tham khảo)
  files                      5,000              14        ít hơn   ✓
  result hash         4379e4c5d9f3    4379e4c5d9f3     không đổi   ✓
  thời gian (ms)                 —            21.6   (tham khảo)

  => giảm 36.5× (cần ≥ 10×)

  kết quả truy vấn (1 hàng):
    ('ACME', 3500, 3068, 2521.1, 4691, 262, 7764750)
```

</details>


---


### Bài B

| | |
|---|---|
| **Nguyên nhân** | Consumer commit offset **trước** khi ghi dữ liệu. Thứ tự thao tác `commit() → crash → write_batch()`. Nếu crash xảy ra tại `maybe_crash()`, batch chưa được ghi nhưng offset đã dịch -> Restart đọc từ offset mới, bỏ qua lô này. Semantics: **at-most-once** (mất dữ liệu). |
| **Cách khắc phục** | (1) Đổi thứ tự: `write_batch() → crash → commit()`. Khi crash, batch đã ghi nhưng offset chưa dịch -> restart đọc lại lô cũ, nó sẽ được phát lại. (2) Để idempotent, thêm `unique` constraint trên `event_id` và dùng `INSERT ... ON CONFLICT (event_id) DO UPDATE SET ...` thay INSERT thuần. Khi message được phát lại cùng `event_id`, `DO UPDATE` cập nhật giá trị mới (nếu nội dung đã sửa sau retry) thay vì tạo hàng trùng. DO UPDATE được chọn thay DO NOTHING vì nó đủ idempotent với schema evolution. |
| **Bằng chứng** | A (bình thường): 20.000 hàng / 20.000 event_id · B (crash ở lô 7, offset = 3.000): tiến trình thoát mã 137 · C (restart): 20.000 hàng / 20.000 event_id · Không mất, không trùng, C == A |

<details>
<summary>Scan B</summary>

```
(.venv) PS E:\AI\Lab\Phase 2\Track2-Day17-K3-01017-NguyenThanhAn> make crash-test

    topic: 20,000 message · batch 500 · giết ở lô 7

    A. chạy một mạch, không sự cố
    [consumer] đã ghi 20,000 message
       -> 20,000 hàng / 20,000 event_id khác nhau

    B. chạy và bị giết ở lô 7
    [consumer] 💥 tiến trình bị giết ở lô 7
       -> tiến trình thoát với mã 137
       -> offset đã commit: 3,000

    C. khởi động lại, chạy nốt
    [consumer] đã ghi 17,000 message
       -> 20,000 hàng / 20,000 event_id khác nhau

    ----------------------------------------------------------
    không mất bản ghi                 ✓
    không trùng bản ghi               ✓
    C == A                            ✓
    ----------------------------------------------------------
    BÀI MỞ RỘNG B: ĐẠT ✓
   và verify (.venv) PS E:\AI\Lab\Phase 2\Track2-Day17-K3-01017-NguyenThanhAn> make verify

    ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
    LAB 17 · make verify
    ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
    run 1/3 … 47.4s
    run 2/3 … 46.2s
    run 3/3 … 39.9s

    BẢNG                  ỔN ĐỊNH          SỐ HÀNG     KỲ VỌNG   GHI CHÚ
    ──────────────────────────────────────────────────────────────────────────
    gold_training_set     ✓ ok              12,480      12,480   ✓
    gold_feature_daily    ✓ ok               9,100       9,100   ✓
    gold_doc_chunks       ✓ ok              31,200      31,200   ✓
    quarantine_tickets    ✓ ok                 312         312   ✓

    CHECKSUM từng lượt
    ──────────────────────────────────────────────────────────────────────────
    gold_training_set     8dd7c98653    8dd7c98653    8dd7c98653   ✓
    gold_feature_daily    3db448685c    3db448685c    3db448685c   ✓
    gold_doc_chunks       92d8e50131    92d8e50131    92d8e50131   ✓
    quarantine_tickets    ebb89036fb    ebb89036fb    ebb89036fb   ✓

    KIỂM TRA KHÁC
    ──────────────────────────────────────────────────────────────────────────
    dbt test                                    ✓ 11/11 pass
    silver_tickets.priority ∈ 1..4, không NULL  ✓ sạch
    quarantine_tickets đúng số bản ghi lỗi      ✓ 312 / 312
    gold_training_set: 1 hàng / 1 ticket        ✓ không lặp
    dashboard rows scanned                      ✓ 5,000,000 → 136,948 (36.5×, cần ≥ 10×)
      số file parquet                           ✓ 5,000 → 14
      kết quả truy vấn không đổi                ✓
    DAG: catchup / max_active_runs              ✓ False / 1

    TỔNG KẾT
    ──────────────────────────────────────────────────────────────────────────
    ✓  1 · gold_training_set idempotent & đúng số hàng
    ✓  2 · gold_feature_daily đủ hàng (dữ liệu về muộn)
    ✓  3 · contract + quarantine + dbt test
    ✓  4 · gold_doc_chunks vẫn ổn định (đối chứng)
    ──────────────────────────────────────────────────────────────────────────
    4/4 tiêu chí đạt cho task extra B
```

</details>

## 5 · Tổng kết

| Nhiệm vụ | Khi tiếp nhận một hệ thống chưa quen, tôi sẽ kiểm tra điều này trước tiên |
|---|---|
| 1 | Incremental model có khai báo `unique_key` không - thiếu nó thì mọi lần chạy lại đều nhân đôi dữ liệu |
| 2 | Điều kiện lọc incremental có dùng lookback window không - `> max` thuần tuý bỏ sót toàn bộ dữ liệu đến muộn |
| 3 | Macro chuẩn hoá có xử lý đủ các dạng biểu diễn của cùng một giá trị không - schema evolution làm nguồn đổi format mà không đổi ý nghĩa |
| A | Dataset file có partition hợp lý và sorted không - filter có sargable (không bọc cột trong function) để engine pruning file bỏ qua mà không cần mở |
| B | Consumer commit offset **sau** ghi dữ liệu không, có dùng idempotent write (`ON CONFLICT DO UPDATE`) không - nếu không, restart sẽ mất dữ liệu hoặc tạo trùng lặp |
