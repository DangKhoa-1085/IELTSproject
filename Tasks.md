# Tasks.md — Kế hoạch phát triển IELTS Online Learning Platform

> **Dự án:** IELTS Online Learning Platform  
> **Stack:** React (Vite) + ASP.NET Core Web API + PostgreSQL (Neon) + Google Gemini AI  
> **Deploy:** Vercel (FE) · Render (BE) · Neon (DB)

---

## Giai đoạn 1 — Nền tảng (Foundation)

**Mục tiêu:** Khởi tạo project, cấu hình môi trường, xác thực người dùng hoạt động đầy đủ.

### Backend
- [ ] Khởi tạo ASP.NET Core Web API solution với cấu trúc thư mục chuẩn (Domain, Application, Infrastructure, API)
- [ ] Kết nối PostgreSQL (Neon), cấu hình EF Core, migrations cơ bản
- [ ] Tích hợp ASP.NET Core Identity (đăng ký, đăng nhập bằng email/password)
- [ ] JWT Access Token + Refresh Token
- [ ] OAuth: Google Login, GitHub Login
- [ ] Phân quyền 3 roles: Student / Teacher / Admin
- [ ] Global exception handling, standard error response

### Frontend
- [ ] Khởi tạo React + Vite project
- [ ] Cấu hình React Router, layout cơ bản (Header, Footer, Sidebar)
- [ ] Trang Register / Login / Forgot Password
- [ ] Tích hợp OAuth button (Google, GitHub)
- [ ] Lưu và refresh JWT token tự động
- [ ] Protected Routes theo role

### ✅ Tiêu chí hoàn thành
> Người dùng có thể đăng ký, đăng nhập (email hoặc OAuth), hệ thống nhận diện đúng role (Student/Teacher/Admin), và truy cập được các route được bảo vệ.

---

## Giai đoạn 2 — Nội dung học tập (Learning Core)

**Mục tiêu:** Hệ thống khóa học, bài học, bài tập hoạt động đầy đủ từ phía Admin/Teacher lẫn Student.

### Backend
- [ ] Models & migrations: Level, Course, Module, Lesson, LessonSection
- [ ] Models & migrations: Exercise, Question, QuestionOption, QuestionTag
- [ ] CRUD API cho Course, Module, Lesson (Teacher/Admin)
- [ ] CRUD API cho Question Bank (Teacher/Admin)
- [ ] API nộp bài & chấm điểm tự động (trắc nghiệm)
- [ ] API lưu kết quả bài làm (QuestionAttempt, UserProgress)
- [ ] Pagination, filtering, sorting cho danh sách

### Frontend
- [ ] Trang danh sách Course, chi tiết Course
- [ ] Trang học Lesson (Theory → Vocabulary → Examples → Exercises → Score → Explanation)
- [ ] Giao diện làm bài tập (Multiple Choice, Fill-in, Matching…)
- [ ] Màn hình kết quả sau nộp bài (score, đáp án đúng, giải thích)
- [ ] Teacher/Admin: trang tạo & quản lý Course, Module, Lesson, Question

### ✅ Tiêu chí hoàn thành
> Teacher/Admin có thể tạo và quản lý khóa học đầy đủ. Student có thể học theo lộ trình Lesson, nộp bài và xem kết quả chấm điểm tự động.

---

## Giai đoạn 3 — 4 Kỹ năng IELTS (Skills Engine)

**Mục tiêu:** Toàn bộ 4 kỹ năng Listening, Reading, Writing, Speaking hoạt động ở mức MVP.

### Backend
- [ ] Listening: upload/stream audio (MP3/WAV), lưu transcript, các dạng câu hỏi chuẩn IELTS
- [ ] Reading: bài đọc dài, các dạng câu hỏi (MCQ, True/False/NG, Matching, Completion)
- [ ] Writing: nộp bài text (Task 1 & Task 2), lưu WritingSubmission
- [ ] Speaking: upload audio, lưu SpeakingSession
- [ ] Object Storage cho file audio/media (cấu hình bucket)

### Frontend
- [ ] Listening player (play/pause, seek, tốc độ 0.75x–2x) + form câu hỏi
- [ ] Reading viewer (bài đọc dài) + form câu hỏi
- [ ] Writing editor (textarea/rich text) + nộp bài
- [ ] Speaking recorder (microphone capture, upload audio)

### ✅ Tiêu chí hoàn thành
> Student có thể hoàn thành đầy đủ một bài luyện tập cho cả 4 kỹ năng: nghe + trả lời, đọc + trả lời, viết + nộp bài text, nói + ghi âm upload.

---

## Giai đoạn 4 — Kiểm tra & Đánh giá (Assessment)

**Mục tiêu:** Placement Test và Mock Test hoạt động đầy đủ, student thấy được tiến độ học tập.

### Backend
- [ ] Placement Test: tạo bài kiểm tra đầu vào, chấm điểm, ước tính band/level
- [ ] Mock Test: tạo đề thi, phân mục (Listening/Reading/Writing/Speaking), timed mode
- [ ] TestAttempt, TestAnswer: lưu lịch sử thi
- [ ] UserProgress: tổng hợp tiến độ theo skill, theo thời gian
- [ ] StudyPlan: lộ trình học cá nhân hóa

### Frontend
- [ ] Màn hình Placement Test (flow: chọn target band → làm bài → xem kết quả → study plan)
- [ ] Màn hình Mock Test (exam mode có đồng hồ đếm giờ)
- [ ] Trang kết quả thi (score, band ước tính, điểm từng kỹ năng)
- [ ] Student Dashboard: Current Band, Target Band, XP, Streak, Today's Recommendation
- [ ] Trang Progress: biểu đồ tiến độ theo thời gian và từng kỹ năng

### ✅ Tiêu chí hoàn thành
> Student mới đăng ký có thể làm Placement Test và nhận Study Plan. Có thể thi Mock Test trong chế độ thi thật (có giờ), xem điểm và theo dõi tiến độ trên dashboard.

---

## Giai đoạn 5 — AI Tutor (AI Integration)

**Mục tiêu:** Tích hợp Gemini AI làm trợ giảng chính: giải thích, chấm Writing, đánh giá Speaking, gợi ý học.

### Backend
- [ ] Cấu hình Gemini API client (AI key chỉ ở backend)
- [ ] Abstraction layer: AI Application Service → Prompt Builder → Gemini Client → Response Validator
- [ ] API: giải thích đáp án sai (`/api/ai/explain`)
- [ ] API: chấm bài Writing Gemini (`/api/ai/evaluate-writing`) → WritingEvaluation
- [ ] API: đánh giá Speaking từ transcript (`/api/ai/evaluate-speaking`) → SpeakingEvaluation
- [ ] API: gợi ý học tiếp (`/api/ai/recommend-study`)
- [ ] Rate limiting per-user cho AI API
- [ ] Lưu AIAssistantSession, AIMessages, AIUsageLogs

### Frontend
- [ ] AI Tutor chat widget (hỏi đáp sau mỗi bài học/bài tập)
- [ ] Hiển thị kết quả chấm Writing AI (band score + nhận xét từng tiêu chí)
- [ ] Hiển thị kết quả đánh giá Speaking AI
- [ ] Gợi ý lesson/skill tiếp theo trên dashboard

### ✅ Tiêu chí hoàn thành
> Student nhận được phản hồi AI sau khi nộp bài Writing và Speaking. Có thể hỏi AI về lỗi sai. Dashboard hiển thị gợi ý học tiếp do AI đề xuất.

---

## Giai đoạn 6 — Teacher & Admin (Management)

**Mục tiêu:** Teacher quản lý lớp và chấm bài; Admin quản lý toàn bộ hệ thống.

### Backend
- [ ] Class, ClassMember: tạo lớp, thêm học viên
- [ ] Assignment, AssignmentSubmission: giao bài và nộp bài
- [ ] TeacherReview: Teacher chấm/nhận xét Writing và Speaking (kết hợp AI)
- [ ] Admin: CRUD users, roles, audit log
- [ ] Admin: quản lý toàn bộ nội dung (courses, questions, mock tests)
- [ ] Admin: xem analytics (số lượng user, lượt học, điểm trung bình)

### Frontend
- [ ] Teacher: trang quản lý lớp học, danh sách học viên
- [ ] Teacher: trang xem & chấm bài nộp của học viên (Writing/Speaking + AI evaluation)
- [ ] Teacher: dashboard báo cáo tiến độ học viên
- [ ] Admin Dashboard: thống kê tổng hợp hệ thống
- [ ] Admin: trang quản lý users, roles
- [ ] Admin: trang quản lý nội dung (courses, questions, mock tests)

### ✅ Tiêu chí hoàn thành
> Teacher tạo được lớp, giao bài, xem bài nộp và chấm điểm (có hỗ trợ AI). Admin quản lý đầy đủ users và nội dung, xem được analytics cơ bản.

---

## Giai đoạn 7 — Gamification & Tiện ích (Engagement)

**Mục tiêu:** Tăng engagement với hệ thống điểm thưởng, thành tích và các tính năng tiện ích.

### Backend
- [ ] XP System: tính và cộng XP sau mỗi hoạt động học
- [ ] Streak: theo dõi chuỗi ngày học liên tiếp
- [ ] Achievement: định nghĩa và trao thành tích tự động
- [ ] Notification: tạo và gửi thông báo trong hệ thống
- [ ] Bookmark, Favorite: lưu lesson/question yêu thích
- [ ] CalendarEvent: lịch học và nhắc nhở

### Frontend
- [ ] Hiển thị XP, Streak, Level trên profile và dashboard
- [ ] Trang Achievements (danh sách thành tích đạt được / chưa đạt)
- [ ] Thông báo (bell icon, danh sách notification)
- [ ] Chức năng Bookmark/Favorite
- [ ] Tích hợp Calendar / lịch ôn tập

### ✅ Tiêu chí hoàn thành
> Student nhận XP và streak sau khi học, mở khóa được thành tích, nhận thông báo, và có thể bookmark bài học yêu thích.

---

## Giai đoạn 8 — Deploy & Production (Launch)

**Mục tiêu:** Hệ thống chạy ổn định trên môi trường production với đầy đủ bảo mật.

- [ ] Cấu hình CI/CD với GitHub Actions
- [ ] Deploy Frontend lên Vercel (với env variables)
- [ ] Deploy Backend lên Render (với env variables)
- [ ] Kết nối Database Neon PostgreSQL production
- [ ] Cấu hình Object Storage cho audio/media
- [ ] Cấu hình CORS, HTTPS, rate limiting production
- [ ] Health check endpoint
- [ ] Structured logging (Serilog hoặc tương đương)
- [ ] Kiểm tra security checklist (HTTPS, JWT validation, input validation, XSS...)
- [ ] Smoke test toàn bộ tính năng MVP trên production

### ✅ Tiêu chí hoàn thành
> Toàn bộ MVP chạy ổn định trên production (Vercel + Render + Neon). Người dùng thực có thể đăng ký, học, làm bài thi, nhận AI feedback mà không có lỗi nghiêm trọng.

---

## Tổng quan Timeline

| Giai đoạn | Nội dung | Mức độ ưu tiên |
|---|---|---|
| 1 | Foundation — Auth, OAuth, Roles | 🔴 Bắt buộc |
| 2 | Learning Core — Course, Lesson, Exercise | 🔴 Bắt buộc |
| 3 | IELTS Skills — Listening, Reading, Writing, Speaking | 🔴 Bắt buộc |
| 4 | Assessment — Placement Test, Mock Test, Progress | 🔴 Bắt buộc |
| 5 | AI Tutor — Gemini Integration | 🔴 Bắt buộc |
| 6 | Teacher & Admin Management | 🟡 Quan trọng |
| 7 | Gamification & Tiện ích | 🟡 Quan trọng |
| 8 | Deploy & Production | 🔴 Bắt buộc |

---

## Phase 2 & 3 (Tương lai)

### Phase 2
- AI adaptive learning nâng cao
- AI-generated course content
- Advanced gamification & Leaderboard
- Advanced analytics
- Calendar reminders, rich notifications
- Media optimization
- Advanced speech analysis
- Personalized mock generation

### Phase 3
- Real-time speaking conversation
- Streaming speech
- Deep AI conversation memory
- Advanced teacher analytics
- Recommendation engine
- Mobile app
- Multi-provider AI fallback
