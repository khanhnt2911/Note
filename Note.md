- release package
npx  nx run {name_package}:nx-release-publish

- package gradle
./gradlew :cdp-gateway-api:clean :cdp-gateway-api:build :cdp-gateway-api:publish

claude mcp add --transport http context7 <https://mcp.context7.com/mcp> --header "CONTEXT7_API_KEY: "
