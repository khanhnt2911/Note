# Sprint 4

- DataPool
  - DataPool Xây dựng chức năng pool chung của Công ty, của khối KD
    - CRM DataPool- Phân quyền BE Hệ thống trạng thái phân bổ -> DONE/DEV
    - CRM DataPool- Phân quyền BE Phân quyền dữ liệu datapool
  - DataPool Chức năng xin datapool chưa được phân bổ
    - CRM DataPool- Phê duyệt Pool BE Sử dụng BPMN cho luồng phê duyệt -> Pending
    - CRM DataPool- Phê duyệt Pool FE Ghép api nghiệp vụ tương ứng -> Pending
    - CRM DataPool- Phê duyệt Pool FE Ghép api với nghiệp vụ CRM -> Pending
  - CRM Bổ sung trường Thông tin KH Cuối -> Processing
    1. Hiện trạng:
      Trong quá trình bán hàng, có nhiều trường hợp NVKD trực tiếp tư vấn và làm việc với khách hàng cuối, nhưng chủ thể ký hợp đồng lại là một khách hàng khác.
      Trước khi có CRM: Nghiệp vụ sẽ tạo thêm một Account cho khách hàng cuối và gán mã tổng với khách hàng ký hợp đồng để phục vụ việc nhập hợp đồng/ID thuê bao.
      Sau khi có CRM: Mỗi khách hàng chỉ có 01 Account duy nhất ⇒ Không thể tạo thêm account để gán mã tổng. Nghiệp vụ hiện đang nhập hợp đồng/thuê bao theo thông tin của chủ thể ký hợp đồng.
      Ví dụ: Chủ thể ký hợp đồng là Viettel, nhưng khách hàng cuối thực tế sử dụng và được NVKD chăm sóc là VTV.
    2. Nhu cầu, mục đích:
      Các khối kinh doanh mong muốn có khả năng phân loại và quản trị doanh thu, kênh, ID... theo khách hàng cuối, nhằm quản lý tổng doanh thu của ecosystem mà khách hàng cuối đó tạo ra.
      Mục đích chính: Tư vấn, chăm sóc và xây dựng chiến lược kinh doanh hướng tới khách hàng cuối, dù hợp đồng ký kết thông qua một pháp nhân khác
    3. Giải pháp đề xuất:
      3.1 Giải pháp: Bổ sung thêm trường dữ liệu "Khách hàng cuối", khai báo ở mức ID thuê bao.
      3.2 Mục đích: Tách rõ thông tin chủ thể ký hợp đồng và khách hàng cuối.
      Đáp ứng nhu cầu phân tích và báo cáo đa chiều, đồng thời giữ đúng nguyên tắc nhập liệu theo thông tin trên hợp đồng.
      3.3 Mô tả chi tiết: Bổ sung thêm trường thông tin "Khách hàng cuối" khi nhập liệu trên các phân hệ (Chi tiết xem trong file đính kèm)Bổ sung trường thông tin KH cuối CRM.docx

  - CRM DataPool notify nhắc nhở tương tác khách hàng -> Processing
  - CRM DataPool- nhắc hẹn đặt lịch FE Chức năng tạo lịch hẹn -> Pending

- Deal
  - CRM Cải tiến giao diện FE View màn Deal
    - Xây dựng pipeline stage -> Pending
    - Xây dựng thông tin chung -> Pending
    - Xây dựng thông tin chi tiế các tab làm việc trong từng stage -> Pending
