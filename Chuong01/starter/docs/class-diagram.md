# Sơ đồ lớp sơ bộ — EduHub

Vẽ bằng Mermaid (hiển thị trực tiếp trên GitHub) hoặc xuất ảnh từ draw.io rồi đặt cạnh file này.
Ghi rõ thuộc tính chính, khoá ngoại (FK) và bội số quan hệ (1, \*, 0..1).

```mermaid
classDiagram
    class Member {
        +Guid Id
        +string Name
        +string Email
        +string StudentCode
        +DateTime JoinedAt
        +Create(...) Member$
        +IsActive() bool
    }

    class Club {
        +Guid Id
        +string Name
        +string Description
        +DateTime CreatedAt
        +List~Member~ Members
        +Create(...) Club$
        +AddMember(Member) void
        +MemberCount() int

    }
    class Event {
        +Guid Id
        +Guid ClubId
        +string Title
        +DateTime Date
        +int Capacity
        +bool IsOnline
        +Create(...) Event$
        +HasCapacity(int) bool

    }
    class Registration {
        +Guid Id
        +Guid MemberId
        +Guid EventId
        +DateTime RegisteredAt
        +string Status
        +Create(...) Registration$
        +Confirm() void
        +Cancel() void
    }

    class CheckIn {
        +Guid Id
        +Guid RegistrationId
        +DateTime CheckedInAt
        +string Method
        +Create(...) CheckIn$
        +Summary() string
    }


    Member "*" -- "*" Club : participates(tham gia)
    Club "1" --> "*" Event : organizes(tổ chức)
    Member "1" -- "*" Registration : registers(đăng ký)
    Event "1" -- "*" Registration : has(có)
    Registration "1" -- "0..1" CheckIn : attendance(tham dự)


```
