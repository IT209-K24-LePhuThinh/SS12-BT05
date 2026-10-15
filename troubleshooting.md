# Troubleshooting

1. Permission Denied: thêm `chmod +x gradlew` trước lệnh test.
2. Authentication Failed: dùng đúng biến `secrets.REGISTRY_TOKEN` hoặc `secrets.GITHUB_TOKEN`.
3. Build Context Error: dùng `context: .` và `file: ./Dockerfile`.
