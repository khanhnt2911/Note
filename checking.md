# danh sách viết lại component

- List lại những component wrap lại những core hiện tại của shell để phù hợp theo đúng system design của designer
- Những component cần phải viết mới
  - XInfoItem
  - XCard
  - XTag
  - XChips
  - XExpand
  - XRadio
  - XCheckbox
  - Bộ icon mới theo thiết kế
- Những component cần phải viết lại (wrap lại cái cũ)
  - button -> name: XButton: Chỉnh sửa lại các props để phù hợp cái các loại button (primary, secondary)
  - tab -> name: XTab
  - TextField -> XInput
  - XSingleSelect/XMultiChoice
  - XListOpt
  
## làm sản phẩm

- đi theo cả đời
- release đi theo từng giai đoạn

## migrate pakd

danh sách các tab làm việc cần được sinh ra
D.COO - CMO - CFO - CEO

Chuyển danh sách thanh một list với - email, thời gian duyệt, managertype

duyệt qua từng bản ghi để tạo thành từng bước
B1: Tạo yêu cầu, sinh tab làm việc
B2: phê duyệt sau đó tiếp diễn lại bước 1

###

Deal: <https://xspace.cmctelecom.vn/customer/deal/view/8852696815664128>

Bước 1: lấy data từ deal theo id
Bước 2: Kiểm tra xem có phải ở PAKD không -> nếu có triển khi tiếp
Bước 3: lấy danh sách process
Bước 4: kiểm tra có đang ở bước của giám đốc khối dữ liệu không
Bước 5: gọi api result và sinh công việc cho bước tiếp theo

- Lấy được request hiện tại ở trạng thái chờ xử lý -> gọi api approve -> tạo tab làm việc -> gọi api approve -> tạo tab làm việc -> gọi approve

#### customer 360

- Tổng quan: ghép công nợ, top 5 tương tác, ticket
- Dịch vụ:
  - overview -> tái sử dụng overview deal (getOverviewDeal)
  - doanh thu theo nhóm dịch vụ
  - dịch vụ sắp hết hạn -> done api in cdp
  - dịch vụ đã ngưng, hủy -> done api in cdp
- chăm sóc: join thêm bảng để lấy member name và last name trong lịch sử chăm sóc khachs hàngd

#### datapool

- Phân quyền chức năng
  - x
- Phân quyền dữ liệu


2159905406;
2159905405;
2159914156;
2159903055;
2159905592;
2159905593;
2159905594;
2159905595;
2159905596;
2159925809;
2159885568;
2159923348;
2159923349;

-- phan bo den khoi
2159886582;
2159886577;

-- phan bo den merchant
2159914692;
2159922094;
2159886582;
2159886577;
2159886580;
2159921880;
2159902487;
2159885386;
2159902974;
2159885567;
2159914279;
2159915150;

-- phan bo den sale
2159914692;
2159922094;
2159902974;
2159885567;
2159914279;
2159915150;