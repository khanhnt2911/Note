# Fix lỗi cert khi chạy project BE và pushlish lib lên nexus

## 1. Nhấn Win + R → nhập mmc → Enter

File → Add/Remove Snap-in... → chọn Certificates → Computer account → Local computer

Mở cây Trusted Root Certification Authorities → Certificates

Tìm GTB Technologies, Inc (39379)

Nhấp phải → All Tasks → Export…

Chọn Base-64 encoded X.509 (.CER)

Lưu thành file: C:\certs\gtb-root.cer

Nếu có “Intermediate Certification Authorities”, export thêm CA trung gian của GTB luôn (đặt tên gtb-int.cer).

## 2. Import vào truststore mặc định của JVM

Mở Command Prompt (Administrator) và chạy:

# import CA gốc

keytool -importcert -alias gtb-root -file

✅ Mật khẩu mặc định của cacerts là changeit. Thay  
Nếu thành công, bạn sẽ thấy:

Certificate was added to keystore

## 3. Kiểm tra lại

Chạy:

keytool -list -cacerts -storepass changeit | findstr /I gtb

Nếu ra dòng có gtb-root, nghĩa là đã import OK.
