# BT05 - Chẩn đoán và khắc phục sự cố Pipeline CI/CD

## 1. Sửa lỗi Permission Denied

Thêm bước cấp quyền thực thi Gradle Wrapper:

```yaml
- name: Grant execute permission for gradlew
  run: chmod +x gradlew
- name: Run tests
  run: ./gradlew test
```

## 2. Sửa lỗi Authentication Failed

Dùng đúng secret `REGISTRY_TOKEN` khi đăng nhập Docker Registry:

```yaml
- name: Login to Docker Registry
  uses: docker/login-action@v3
  with:
    username: ${{ secrets.REGISTRY_USER }}
    password: ${{ secrets.REGISTRY_TOKEN }}
```

## 3. Sửa lỗi Build Context Error

Chỉ định đúng build context và Dockerfile:

```yaml
- name: Build and push Docker image
  uses: docker/build-push-action@v5
  with:
    context: .
    file: ./Dockerfile
    push: true
```

## 4. Kết quả pipeline sau khi sửa

```text
Broken Pipeline
  ✓ Checkout code
  ✓ Grant execute permission for gradlew
  ✓ Run tests
    BUILD SUCCESSFUL in 41s
  ✓ Login to Docker Registry
    Login Succeeded
  ✓ Build and push Docker image
    #7 exporting to image
    #7 pushing layers
    #7 DONE

Pipeline completed successfully
```

## 5. troubleshooting.md

```text
1. Permission Denied: thêm chmod +x gradlew trước khi chạy ./gradlew test.
2. Authentication Failed: kiểm tra đúng tên secret REGISTRY_TOKEN.
3. Build Context Error: đặt context là . và file là ./Dockerfile.
```
