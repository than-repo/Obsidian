Alias primitives: 
Alias primitives trong TypeScript đề cập đến việc sử dụng **type alias** để tạo bí danh (alias) cho các kiểu dữ liệu cơ bản (primitives), như string, number, boolean, null, v.v. Đây là một tính năng của type (không phải interface), giúp code dễ đọc hơn bằng cách đặt tên ý nghĩa cho kiểu đơn giản.
### Ví Dụ:

typescript

```
type Username = string;  // Alias cho primitive string
type Age = number;       // Alias cho primitive number

const user: Username = "Alice";  // Tương đương string, nhưng ý nghĩa hơn
```