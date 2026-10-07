# AGENTS.md — Hướng dẫn cho AI Agent

## 1. Tổng quan dự án

**Tên dự án:** IELTS Online Learning Platform  
**Mục tiêu:** Nền tảng học và luyện IELTS online toàn diện, AI Tutor tích hợp Gemini.

### Stack chính
| Layer | Công nghệ |
|---|---|
| Frontend | React + Vite (TypeScript) |
| Backend | ASP.NET Core 8 Web API (C#) |
| Database | PostgreSQL — hosted trên Neon |
| ORM | Entity Framework Core |
| Auth | ASP.NET Core Identity + JWT + Refresh Token |
| OAuth | Google, GitHub |
| AI | Google Gemini API |
| File Storage | Object Storage (S3-compatible) |
| Deploy FE | Vercel |
| Deploy BE | Render |

---

## 2. Cấu trúc thư mục dự kiến

```
/
├── frontend/          # React + Vite app
│   ├── src/
│   │   ├── api/       # API client, axios instances
│   │   ├── components/
│   │   ├── pages/
│   │   ├── hooks/
│   │   ├── store/     # State management
│   │   ├── types/
│   │   └── utils/
│   └── ...
│
├── backend/           # ASP.NET Core Web API
│   ├── IeltsApp.API/
│   ├── IeltsApp.Application/
│   ├── IeltsApp.Domain/
│   ├── IeltsApp.Infrastructure/
│   └── IeltsApp.sln
│
├── AGENTS.md
├── Tasks.md
├── IELTS_WEBSITE_SPEC.md
└── .gitignore
```

---

## 3. Quy tắc code — Backend (C# / ASP.NET Core)

### Kiến trúc
- Tuân thủ **Clean Architecture**: Domain → Application → Infrastructure → API.
- Không để business logic trong Controller. Controller chỉ nhận request và gọi Application Service.
- Dùng **DTO** cho tất cả request/response, không expose Entity trực tiếp.
- Dùng **Repository pattern** khi cần tách biệt data access phức tạp.
- **AI key** (`Gemini__ApiKey`) chỉ nằm ở backend, không bao giờ trả về client.

### Conventions
- Tên class: `PascalCase`. Tên property: `PascalCase`. Tên biến/tham số: `camelCase`.
- Tên API endpoint: `kebab-case` (ví dụ: `/api/mock-tests`).
- Mỗi entity có `Id (Guid)`, `CreatedAt`, `UpdatedAt`.
- Async/await cho tất cả I/O operations.
- Dùng `cancellationToken` trong các method async service.

### API Response chuẩn
```json
{
  "success": true,
  "data": { },
  "message": "OK",
  "errors": []
}
```

### Migrations
- Mỗi thay đổi schema phải có migration riêng với tên mô tả rõ ràng.
- Không sửa migration đã chạy trên production.

### Security
- Không commit secrets, connection string, API key vào Git.
- Tất cả secrets qua environment variables / `appsettings.{env}.json` (file này trong `.gitignore`).
- Rate limiting bắt buộc với các AI endpoint.
- Validate tất cả input (FluentValidation hoặc DataAnnotations).

---

## 4. Quy tắc code — Frontend (React + Vite + TypeScript)

### Conventions
- Component: `PascalCase`. Hook: `use` prefix + `camelCase`. File: `kebab-case.tsx`.
- Tách logic vào custom hook, không viết business logic dài trong component.
- Dùng `axios` với interceptor để tự động đính kèm JWT và xử lý refresh token.
- Lazy loading tất cả route-level component (`React.lazy + Suspense`).

### State management
- Dùng **React Query (TanStack Query)** cho server state (fetch, cache, invalidate).
- Dùng **Zustand** hoặc **Context API** cho global UI state (auth user, theme...).

### Styling
- Dùng **CSS Modules** hoặc **Vanilla CSS**. Không dùng inline style phức tạp.
- Thiết kế phải responsive (mobile-first).

### Environment variables
- Tất cả env var FE phải bắt đầu bằng `VITE_`.
- Không commit file `.env`, `.env.local`, `.env.production`.

---

## 5. Quy tắc AI Integration (Gemini)

- Mọi call Gemini đều đi qua `AIApplicationService` → `PromptBuilder` → `GeminiClient` → `ResponseValidator`.
- Không gọi Gemini trực tiếp từ Controller.
- Mỗi loại tác vụ AI có Prompt template riêng (Writing eval, Speaking eval, Explain, Recommend...).
- Luôn validate response từ Gemini trước khi lưu DB.
- Xử lý timeout và retry ở mức an toàn (max 3 retry với exponential backoff).
- Log tất cả AI request/response vào `AIUsageLogs`.

---

## 6. Quy tắc Git

### Commit message format
```
<type>(<scope>): <mô tả ngắn>

feat(auth): add Google OAuth login
fix(writing): correct band score calculation
chore(deps): update EF Core to 8.0.5
docs(api): update Swagger annotations
```

**Types:** `feat`, `fix`, `refactor`, `test`, `docs`, `chore`, `style`

### Branch naming
```
feature/<tên-tính-năng>
fix/<tên-lỗi>
chore/<tên-công-việc>
```

### Quy tắc bắt buộc
- **Không commit trực tiếp lên `main`.**
- Mỗi feature có branch riêng.
- Không commit file secrets, `.env`, build artifacts, `node_modules`, `bin/`, `obj/`.

---

## 7. Các lệnh hay dùng

### Backend
```bash
# Chạy API
cd backend/IeltsApp.API
dotnet run

# Thêm migration
dotnet ef migrations add <TenMigration> --project ../IeltsApp.Infrastructure

# Apply migration
dotnet ef database update --project ../IeltsApp.Infrastructure

# Chạy tests
dotnet test
```

### Frontend
```bash
# Dev server
cd frontend
npm run dev

# Build production
npm run build

# Lint
npm run lint
```

---

## 8. Checklist trước khi commit

- [ ] Không có secrets/API key trong code.
- [ ] DTO được dùng thay vì Entity trực tiếp.
- [ ] Endpoint mới có validation và authorization.
- [ ] Không có `Console.WriteLine` hay `console.log` thừa.
- [ ] Migration được tạo nếu có thay đổi DB schema.
- [ ] Không có `node_modules/`, `bin/`, `obj/` trong commit.
