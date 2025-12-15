- release package
npx  nx run {name_package}:nx-release-publish

- package gradle
./gradlew :cdp-gateway-api:clean :cdp-gateway-api:build :cdp-gateway-api:publish

claude mcp add --transport http context7 <https://mcp.context7.com/mcp> --header "CONTEXT7_API_KEY: "

Deploy Xspace-customer lên môi trường PROD

Thời gian: 18h00 10/12/2025
Mục đích: Sửa lỗi tự động chuyển tab làm việc tại màn hình Deal trên Xspace khi chuyển qua tab khác của trình duyệt
Service: xspace-customer
Git: <https://git.cmctelecom.vn/cds/dx/frontends/xspace/xspace-customer>
Tag: prod-20251210-01
