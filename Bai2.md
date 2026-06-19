### Bài 2 — Tối ưu Prompt: Giải nghĩa Stack Trace và gỡ lỗi (100 điểm)

Vai trò: Tôi cần một chuyên gia gỡ lỗi Java (Java Debugger).

Ngữ cảnh (mã nguồn gây lỗi và Stack Trace):

Mã lỗi:

```java
import java.util.List;

public class UserManager {

    private List<String> users; // Lỗi: Danh sách chưa được khởi tạo (null)

    public void addUser(String user) {
        users.add(user); // Dòng gây lỗi NullPointerException
    }

}
```

Stack Trace:

```
Exception in thread "main" java.lang.NullPointerException: Cannot invoke "java.util.List.add(Object)" because "this.users" is null
    at UserManager.addUser(UserManager.java:7)
    at Main.main(Main.java:6)
```

Yêu cầu (theo cấu trúc 5 thành phần):

1) Vai trò: Bạn hãy đóng vai một chuyên gia gỡ lỗi Java (Java Debugger).
2) Mục tiêu: Phân tích chính xác Root Cause của NullPointerException, chỉ ra dòng gây lỗi, và đề xuất sửa chữa an toàn nhất.
3) Ngữ cảnh: Đính kèm mã nguồn và Stack Trace ở trên.
4) Hành động cần thực hiện: Giải thích nguyên nhân gốc rễ, nêu các lựa chọn khắc phục, và cung cấp đoạn mã Java sửa an toàn (khởi tạo `users` bằng `ArrayList`) mà không phá vỡ tính bao đóng (encapsulation).
5) Ràng buộc: Ghi rõ sửa chỉ khởi tạo danh sách trong lớp (`private`), cung cấp constructor hợp lệ, và không chuyển trường `users` sang `public`.

Prompt tối ưu (dùng để gửi cho AI):

"Bạn là một chuyên gia gỡ lỗi Java (Java Debugger). Tôi gặp NullPointerException khi gọi `UserManager.addUser(...)`. Tôi gửi mã nguồn và Stack Trace đầy đủ (bên dưới). Hãy:

- Xác định chính xác Root Cause và dòng gây lỗi trong mã.
- Giải thích vì sao lỗi xảy ra theo ngữ cảnh OOP (bao gồm nguyên nhân vì `users` null).
- Đề xuất cách sửa an toàn nhất: khởi tạo `users` bằng `new ArrayList<>()` trong constructor, giữ `users` là `private`, và cung cấp getter trả bản sao để giữ encapsulation.
- Trả về đoạn mã Java hoàn chỉnh, compile được, và tuân thủ ràng buộc trên.

Mã và Stack Trace:

```java
import java.util.List;

public class UserManager {

    private List<String> users; // Lỗi: Danh sách chưa được khởi tạo (null)

    public void addUser(String user) {
        users.add(user); // Dòng gây lỗi NullPointerException
    }

}
```

```
Exception in thread "main" java.lang.NullPointerException: Cannot invoke "java.util.List.add(Object)" because "this.users" is null
    at UserManager.addUser(UserManager.java:7)
    at Main.main(Main.java:6)
```
"

Đoạn mã Java hoàn chỉnh và an toàn (đầu ra yêu cầu):

```java
import java.util.List;
import java.util.ArrayList;

public class UserManager {

    private List<String> users;

    // Khởi tạo trong constructor để tránh NullPointerException
    public UserManager() {
        this.users = new ArrayList<>();
    }

    public synchronized void addUser(String user) {
        if (user == null) return;
        users.add(user);
    }

    // Trả về bản sao để bảo vệ encapsulation
    public List<String> getUsers() {
        return new ArrayList<>(users);
    }

}
```