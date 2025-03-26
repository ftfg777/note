
**PreAuthorize**
메서드 실행 전에 권한을 확인해서 허용된 사용자만 접근 가능
```Java
@PreAuthorize("hasRole('ADMIN')")
public void deleteUser() {
    // 관리자가 아니면 이 메서드를 실행할 수 없음
}
```

**RequireAuthentication**
인증된 사용자만 접근 가능하지만, 권한까지는 따지지 않음
```Java
@RequireAuthentication
public void viewProfile() {
    // 로그인한 사용자라면 누구나 접근 가능
}
```

