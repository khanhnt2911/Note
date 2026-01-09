# Luồng tạo một flow

## Phân quyền tạo luồng

1. Tạo code flow với cặp

- BPMN_FLOW_TYPE
- theo từng modules: "customer-request"

2. Tạo thêm một vai trò trong phân hệ process tương ứng với modules của bạn

- Tạo policy với phân hệ tương ứng với config
config: {
	"default.scope.domain": true,
	"domain": [
		{
			"type": "CUSTOMER-REQUEST-TYPE",
			"column": "request_type"
		}
	]
}

code: customer-request-type

- sau khi tạo xong -> ấn vào bánh răng (setup) -> phạm vi dữ liệu -> appdomain -> thêm mới -> tìm kiếm tên theo từng modules bạn mới đặt tên vd: "customer-request"

3. Phân quyền người dùng

- Tìm kiếm người muốn phân quyền tạo luồng -> tìm phân hệ process -> thêm vai trò bạn vừa mới tạo

--> BOOM -> chờ đợi 30s và tiến hành tạo luồng

4. cấu hình phạm vi quy trình

- chọn phạm vi quy trình với nhóm chương trình bạn mong muốn -> ban hành -> có hiệu lực

NOTE: nếu ban hành r hủy thì sẽ phải tạo luồng mới, không sử dụng lại được luồng đã hủy ban hành
