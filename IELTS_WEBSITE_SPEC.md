# IELTS Online Learning Platform — Product & Technical Specification

> **Trạng thái:** Draft đặc tả tổng thể  
> **Mục tiêu:** Xây dựng nền tảng học và luyện IELTS online toàn diện, từ cơ bản đến nâng cao, có AI làm trợ giảng chính.  
> **Định hướng:** Đủ mạnh để làm đồ án lớn và có kiến trúc thực tế để deploy production.

## 1. Tổng quan

Website là nền tảng IELTS cho mọi trình độ, kết hợp học theo khóa học, luyện 4 kỹ năng, Grammar/Vocabulary/Pronunciation, ngân hàng câu hỏi, Mock Test, Placement Test, theo dõi tiến bộ, gamification và AI Tutor.

**Không triển khai bán khóa học/thanh toán trong scope hiện tại.**

## 2. Roles

### Student
- Học từ cơ bản đến nâng cao.
- Làm bài tập, mock test.
- Nộp Writing/Speaking.
- Nhận AI feedback.
- Theo dõi tiến độ.
- Study Plan cá nhân.
- XP/Streak/Achievements.
- Bookmark/Favorite/Search/Notifications/Calendar.

### Teacher
- Tạo/chỉnh sửa nội dung theo quyền.
- Tạo exercise/question/assignment.
- Quản lý lớp.
- Theo dõi học viên.
- Review/chấm Writing và Speaking.
- Review kết quả AI.
- Xem báo cáo.

### Admin
- Quản lý user/roles.
- Quản lý courses/modules/lessons/questions/mock tests.
- Quản lý teachers/classes.
- Quản lý achievements/notifications.
- Quản lý AI configuration.
- Xem analytics toàn hệ thống.

---

# 3. Phạm vi học tập

## 3.1 Level

```text
Beginner
Elementary
Pre-Intermediate
Intermediate
Upper-Intermediate
Advanced
IELTS 6.5+
IELTS 7.5+
```

Mục tiêu bao phủ toàn bộ từ nền tảng đến IELTS nâng cao.

## 3.2 Skills

### IELTS
- Listening
- Reading
- Writing
- Speaking

### Supporting Skills
- Grammar
- Vocabulary
- Pronunciation
- IELTS Tips/Strategies

---

# 4. Cấu trúc nội dung

Mô hình đề xuất:

```text
Level
  └── Course
      └── Module
          └── Lesson
              ├── Theory
              ├── Vocabulary
              ├── Examples
              ├── Exercises
              ├── Score
              └── Explanation
```

Một lesson đi theo:

```text
Theory
→ Vocabulary
→ Examples
→ Exercises
→ Submit
→ Score
→ Correct Answers
→ Detailed Explanation
→ AI Tutor
```

### Quy tắc học
- Course nền tảng có thể học tuần tự.
- Course luyện kỹ năng có thể học tự do.
- Có cờ `isSequential` để cấu hình.

---

# 5. Placement Test

Student mới có thể làm bài kiểm tra đầu vào:

```text
Register/Login
→ Chọn Target Band
→ Placement Test
→ Phân tích
→ Estimated Level/Band
→ Personalized Study Plan
```

Kiểm tra chính:
- Grammar
- Vocabulary
- Reading
- Listening

Có thể mở rộng:
- Writing sample
- Speaking sample

Kết quả:
- Level hiện tại.
- Điểm từng kỹ năng.
- Band ước tính.
- Điểm yếu.
- Lộ trình đề xuất.

---

# 6. Student Dashboard

Dashboard hiển thị:

```text
Current Band
Target Band
Exam Date
Listening
Reading
Writing
Speaking
XP
Streak
Lessons Completed
Study Time
Today's Recommendation
```

Student đặt:
- Target Band.
- Exam Date.
- Daily Study Goal.

Hệ thống/AI đề xuất:
- Lesson tiếp theo.
- Skill cần ưu tiên.
- Vocabulary cần ôn.
- Grammar cần cải thiện.
- Mock Test nên làm.

---

# 7. Listening

Hỗ trợ:
- MP3/WAV/M4A; video khi cần.
- Transcript.
- Multiple Choice.
- Matching.
- Form/Note/Sentence/Summary completion.
- Map/Plan/Diagram Labelling.
- Short Answer.

Player:
- Play/Pause
- Seek
- 0.75x / 1x / 1.25x / 1.5x / 2x

Sau nộp:
```text
Score
→ Correct Answers
→ Explanation
→ Transcript
→ Mistake Analysis
→ AI Tutor
```

---

# 8. Reading

Hỗ trợ:
- Multiple Choice
- True/False/Not Given
- Yes/No/Not Given
- Matching Headings
- Matching Information/Features
- Sentence/Summary/Note/Table/Flow-chart completion
- Diagram Label
- Short Answer

Mock Reading mặc định:
- 3 passages
- 40 questions
- 60 phút

Lưu được dữ liệu:
- User answer
- Correct answer
- Time spent
- Question type
- Topic

---

# 9. Writing

## Task 1
- Line graph
- Bar chart
- Pie chart
- Table
- Process
- Map
- Mixed charts

## Task 2
- Opinion
- Discussion
- Advantages/Disadvantages
- Problem/Solution
- Two-part question

## AI Evaluation

Đánh giá 4 tiêu chí:
- Task Response / Task Achievement
- Coherence & Cohesion
- Lexical Resource
- Grammatical Range & Accuracy

Ví dụ:

```text
Estimated Band: 6.0
Task Response: 6.0
Coherence & Cohesion: 5.5
Lexical Resource: 6.0
Grammar: 5.5
```

AI phân tích:
- Grammar errors.
- Vocabulary errors.
- Unnatural sentences.
- Repetition.
- Collocation.
- Coherence.
- Sentence structure.

Mỗi lỗi:
```text
Original Sentence
→ Problem
→ Explanation
→ Corrected Sentence
→ Better Version
```

Có `Band Improvement Suggestions`:
```text
Current: 5.5
Target: 6.5

Need to improve:
- Grammar accuracy
- Vocabulary variety
- Paragraph development
- Coherence
```

Teacher có thể review sau AI.

---

# 10. Speaking

Đầy đủ:
- Part 1
- Part 2
- Part 3
- Cue Card
- Preparation Timer
- Speaking Timer

Luồng:
```text
Question
→ Preparation
→ Speaking
→ Recording
→ Speech-to-Text
→ AI Analysis
→ Band Estimate
```

AI phân tích:
- Fluency
- Coherence
- Vocabulary
- Grammar
- Pronunciation
- Fillers
- Repetition
- Sentence errors

Có `AI Speaking Conversation` để mô phỏng examiner.

---

# 11. Exercise Engine

Thiết kế generic để hỗ trợ:
- Multiple Choice
- Multiple Select
- True/False/Not Given
- Yes/No/Not Given
- Fill in the Blank
- Short Answer
- Matching
- Ordering
- Sentence Completion
- Summary Completion
- Speaking Response
- Writing Response

Question metadata:
```text
Question
Options
Correct Answer
Explanation
Skill
Difficulty
Topic
Tags
Points
Time Limit
Media
Transcript
```

---

# 12. Question Bank

Admin/Teacher có thể:
- Create/Edit/Delete/Duplicate
- Tag
- Filter
- Import/Export
- Gán skill
- Gán topic
- Gán difficulty

Difficulty:
- Easy
- Medium
- Hard
- Very Hard

Topic ví dụ:
- Environment
- Technology
- Education
- Health
- Society
- Work
- Travel
- Science

---

# 13. Mock Test

Có 2 chế độ.

## Practice Mode
- Không bắt buộc timer.
- Explanation.
- Retry.

## Exam Mode
- Timer.
- Không xem đáp án trước.
- Tự submit khi hết giờ.
- Mô phỏng IELTS format.

Kết quả:
```text
Overall Band
Listening
Reading
Writing
Speaking
Time Used
Accuracy
Question Breakdown
Weak Topics
Suggested Lessons
```

Lưu lịch sử để biểu diễn:
```text
Mock #01 → 5.5
Mock #02 → 5.5
Mock #03 → 6.0
Mock #04 → 6.5
```

---

# 14. AI IELTS Tutor

AI là **trợ giảng chính**, không chỉ là chatbot.

## Chức năng
- Giải thích bài học.
- Giải thích đáp án.
- Tạo ví dụ.
- Tạo bài tập.
- Tạo mini test.
- Tạo flashcards.
- Chữa lỗi.
- Tạo Writing topics.
- Tạo Speaking questions.
- Phân tích Writing.
- Phân tích Speaking.
- Đề xuất học tập.

## AI Chat

Có màn hình riêng:
```text
Student → hỏi
AI → giải thích
Student → yêu cầu bài tập
AI → tạo bài
Student → gửi đáp án
AI → chấm + giải thích
```

AI cũng xuất hiện trực tiếp trong lesson.

## AI Learning Profile

```text
Current Level
Estimated Band
Weak Skills
Grammar Weaknesses
Vocabulary Gaps
Common Errors
Study Habits
Recommended Activities
```

AI dùng lịch sử học tập để cá nhân hóa.

## AI Content Generation

AI có thể tạo:
- Vocabulary exercises
- Grammar exercises
- Reading questions
- Listening questions
- Speaking questions
- Writing topics
- Flashcards
- Mini tests

Nội dung chính thức nên đi:
```text
Draft → Teacher Review → Published
```

## AI Provider

Dùng **Google Gemini**.

Tạo abstraction:
```text
IAssistantService
    ↓
GeminiAssistantService
```

Không gọi Gemini trực tiếp từ browser.

API key chỉ nằm ở backend environment.

## AI ngôn ngữ

Hỗ trợ cả:
- Vietnamese
- English

Ví dụ:
- Grammar explanation: Việt + English.
- Speaking conversation: English.
- Feedback: Việt + English tùy ngữ cảnh.

---

# 15. AI Quality/Safety

- Prompt template versioning.
- Output validation.
- Rate limiting.
- Token/usage tracking.
- Timeout/retry.
- Logging.
- Teacher/Admin review cho nội dung cần publish.
- AI không tự ghi đè điểm chính thức nếu chưa qua rule/teacher review.

---

# 16. Gamification

## XP
Nhận XP khi:
- Hoàn thành lesson.
- Hoàn thành exercise.
- Hoàn thành mock test.
- Duy trì streak.
- Achievement.

## Levels
Ví dụ:
```text
Level 1 → Beginner Learner
Level 10 → IELTS Explorer
Level 20 → IELTS Challenger
Level 30 → IELTS Master
```

## Streak
Theo dõi số ngày học liên tục.

## Achievement
Ví dụ:
- First Lesson
- First Mock Test
- 7-Day Streak
- 30-Day Streak
- 100 Exercises
- Writing Master
- Listening Master

## Leaderboard
Theo:
- XP tuần
- XP tháng
- XP tổng

Có thể bật/tắt bằng cấu hình Admin.

---

# 17. Search / Bookmark / Favorites / Calendar / Notifications

Có:
- Global Search
- Bookmark lesson
- Bookmark question
- Favorites
- Notification Center
- Study Calendar
- Learning Reminders

Không có trong scope:
- Personal study notes
- Dark mode

---

# 18. Teacher Module

## Content
Teacher có quyền:
- Create lesson.
- Create exercise/question.
- Create assignment.
- Review AI-generated content.

## Class

```text
Class
├── Teacher
├── Students
├── Courses
├── Assignments
├── Progress
└── Reports
```

## Student monitoring
- Current level.
- Band.
- Skill scores.
- Learning activity.
- Exercise performance.
- Mock result.
- Weak topics.
- Assignment status.

## Teacher review
```text
Student submits
→ AI evaluates
→ Teacher reviews
→ Teacher can edit score/comments
→ Final result
```

AI score không tự động ghi đè điểm teacher.

---

# 19. Admin Module

Dashboard:
- Total Users
- Active Users
- New Users
- Students
- Teachers
- Courses
- Lessons
- Questions
- Mock Tests
- Completed Tests
- Average Band
- AI Requests
- AI Usage/Cost metrics
- Most difficult questions
- Most common mistakes

Quản lý:
```text
Users
Roles
Courses
Modules
Lessons
Questions
Question Bank
Mock Tests
Teachers
Classes
Achievements
Notifications
AI Config
Reports
System Settings
```

---

# 20. Authentication & Authorization

Hỗ trợ:
- Email + Password
- Google OAuth
- GitHub OAuth
- Email verification
- Forgot password
- Reset password

Dùng:
- ASP.NET Core Identity
- JWT Access Token
- Refresh Token
- Role-based authorization

Roles:
```text
Student
Teacher
Admin
```

Khuyến nghị:
- Access token ngắn hạn.
- Refresh token rotation/revocation.
- Secure HTTP-only cookie cho refresh token nếu kiến trúc phù hợp.

---

# 21. File & Media Storage

Không lưu audio/video lớn trực tiếp trong PostgreSQL.

Database lưu:
- metadata
- URL/object key

Object storage có thể dùng:
- Cloudflare R2
- Cloudinary
- AWS S3
- Supabase Storage

Kiến trúc:
```text
React
→ ASP.NET Core API
→ Object Storage

PostgreSQL
→ metadata + object key
```

---

# 22. Analytics & Progress

Lưu:
- Question attempts
- Correct/incorrect
- Time spent
- Skill performance
- Topic performance
- Error patterns
- Mock history
- Study sessions

Ví dụ:
```text
Reading
Matching Headings → 48%
TFNG → 61%
Summary Completion → 74%

Weakest Topic → Environment
Common Error → Inference questions
```

Dữ liệu này là input cho AI Tutor.

---

# 23. User Flows

## First-time Student
```text
Landing
→ Register/Login
→ Target Band
→ Exam Date (optional)
→ Placement Test
→ Result
→ Personalized Study Plan
→ Dashboard
```

## Normal Learning
```text
Dashboard
→ Recommended Lesson
→ Theory
→ Vocabulary
→ Examples
→ Exercises
→ Score
→ Explanation
→ AI Tutor
→ Progress Updated
```

## Writing
```text
Choose Task
→ Write
→ Submit
→ Gemini Evaluation
→ Band + Criteria
→ Corrections
→ Improvement Plan
→ Optional Teacher Review
```

## Speaking
```text
Choose Test
→ Part 1
→ Part 2
→ Part 3
→ Record
→ Speech-to-Text
→ AI Analysis
→ Band Estimate
→ Feedback
```

## Mock Test
```text
Select
→ Practice/Exam Mode
→ Test
→ Submit/Auto Submit
→ Result
→ Question Analysis
→ Weakness Analysis
→ Recommended Lessons
```

---

# 24. Frontend Pages

## Public
```text
/
/about
/courses
/courses/:id
/login
/register
/forgot-password
/reset-password
```

## Student
```text
/dashboard
/placement-test
/study-plan
/courses/:id/learn
/lessons/:id
/practice
/listening
/reading
/writing
/speaking
/mock-tests
/mock-tests/:id
/results/:id
/progress
/calendar
/bookmarks
/favorites
/achievements
/leaderboard
/notifications
/ai-tutor
/profile
/settings
```

## Teacher
```text
/teacher/dashboard
/teacher/classes
/teacher/classes/:id
/teacher/students
/teacher/courses
/teacher/lessons
/teacher/questions
/teacher/assignments
/teacher/reviews
/teacher/reports
```

## Admin
```text
/admin/dashboard
/admin/users
/admin/roles
/admin/courses
/admin/modules
/admin/lessons
/admin/questions
/admin/question-bank
/admin/mock-tests
/admin/teachers
/admin/classes
/admin/achievements
/admin/notifications
/admin/ai
/admin/reports
/admin/settings
```

---

# 25. Backend Architecture

Khuyến nghị ASP.NET Core Web API với separation:

```text
src/
├── API/
├── Application/
├── Domain/
├── Infrastructure/
└── Shared/
```

Có thể tổ chức feature:
```text
Features/
├── Auth
├── Users
├── Courses
├── Lessons
├── Exercises
├── Questions
├── MockTests
├── Writing
├── Speaking
├── AI
├── Progress
├── Gamification
├── Notifications
└── Admin
```

Khuyến nghị kết hợp modular feature với separation Domain/Application/Infrastructure.

---

# 26. Database — PostgreSQL / Neon

Database: **PostgreSQL**, deploy trên **Neon**.

## Identity
- User
- Role
- UserRole
- ExternalLogin
- RefreshToken

## Learning
- Level
- Course
- Module
- Lesson
- LessonSection
- Vocabulary
- GrammarTopic
- Example

## Exercise
- Exercise
- Question
- QuestionOption
- QuestionTag
- Answer
- Explanation
- MediaAsset

## Assessment
- PlacementTest
- PlacementAttempt
- MockTest
- MockTestSection
- MockTestQuestion
- TestAttempt
- TestAnswer

## Writing/Speaking
- WritingSubmission
- WritingEvaluation
- WritingFeedback
- SpeakingSession
- SpeakingTranscript
- SpeakingEvaluation

## Progress
- UserProgress
- LessonProgress
- SkillProgress
- QuestionAttempt
- StudySession
- StudyPlan

## Teacher
- Class
- ClassMember
- Assignment
- AssignmentSubmission
- TeacherReview

## AI
- AIAssistantSession
- AIMessage
- AIEvaluation
- AIUsageLog
- AIPromptTemplate

## Gamification
- XPTransaction
- UserLevel
- Achievement
- UserAchievement
- Streak
- LeaderboardSnapshot

## System
- Notification
- Bookmark
- Favorite
- CalendarEvent
- AuditLog

---

# 27. Core Relationships

```text
User
├── UserProgress
├── StudyPlan
├── QuestionAttempt
├── TestAttempt
├── WritingSubmission
├── SpeakingSession
├── AIConversation
├── XPTransaction
├── Achievement
└── Notifications

Course
└── Module
    └── Lesson
        └── Exercise
            └── Question

MockTest
└── MockTestSection
    └── MockTestQuestion

Class
├── Teacher
├── Students
└── Assignments
```

---

# 28. API Modules

```text
/api/auth
/api/users
/api/courses
/api/modules
/api/lessons
/api/exercises
/api/questions
/api/vocabulary
/api/grammar
/api/listening
/api/reading
/api/writing
/api/speaking
/api/mock-tests
/api/placement-tests
/api/progress
/api/study-plan
/api/ai
/api/teacher
/api/classes
/api/assignments
/api/notifications
/api/bookmarks
/api/gamification
/api/admin
```

AI endpoints:
```text
POST /api/ai/chat
POST /api/ai/explain
POST /api/ai/generate-exercise
POST /api/ai/evaluate-writing
POST /api/ai/evaluate-speaking
POST /api/ai/recommend-study
POST /api/ai/analyze-progress
```

API nguyên tắc:
- RESTful.
- DTO, không expose trực tiếp Entity.
- Validation.
- Auth/Authorization.
- Pagination.
- Filtering.
- Sorting.
- Search.
- Standard error response.
- Rate limiting AI.
- Logging.

---

# 29. AI Processing Architecture

```text
React
→ ASP.NET Core API
→ AI Application Service
→ Prompt Builder
→ Gemini Client
→ Response Validator
→ Domain Result
→ Database
→ React
```

AI key chỉ nằm ở backend.

---

# 30. Speaking Technical Flow

Đề xuất:

```text
Browser Microphone
→ Audio Capture
→ Upload/Streaming API
→ Speech-to-Text Layer
→ Transcript
→ Gemini Evaluation
→ Speaking Evaluation
```

Speech-to-Text cũng nên có abstraction để có thể thay provider sau này.

---

# 31. Deployment

Kiến trúc:

```text
                  INTERNET
                     │
                     ▼
              ┌──────────────┐
              │    Vercel    │
              │ React/Vite   │
              └──────┬───────┘
                     │ HTTPS
                     ▼
              ┌──────────────┐
              │    Render    │
              │ ASP.NET Core │
              │   Web API    │
              └──────┬───────┘
                     │
          ┌──────────┴──────────┐
          ▼                     ▼
   ┌──────────────┐      ┌──────────────┐
   │     Neon     │      │    Gemini    │
   │ PostgreSQL   │      │     API      │
   └──────────────┘      └──────────────┘
          │
          ▼
   ┌──────────────┐
   │ Object Store │
   │ Audio/Video  │
   └──────────────┘
```

- Frontend: Vercel.
- Backend: Render.
- Database: Neon PostgreSQL.
- AI: Google Gemini.
- Media: Object Storage.

---

# 32. Environment Variables

## Frontend
```env
VITE_API_BASE_URL=
VITE_GOOGLE_CLIENT_ID=
VITE_GITHUB_CLIENT_ID=
```

## Backend
```env
ConnectionStrings__DefaultConnection=
Jwt__Secret=
Jwt__Issuer=
Jwt__Audience=
Jwt__AccessTokenMinutes=
Jwt__RefreshTokenDays=
Google__ClientId=
Google__ClientSecret=
GitHub__ClientId=
GitHub__ClientSecret=
Gemini__ApiKey=
Storage__Bucket=
Storage__AccessKey=
Storage__SecretKey=
Storage__Endpoint=
```

---

# 33. Security

Bắt buộc:
- HTTPS.
- ASP.NET Identity password hashing.
- JWT validation.
- Refresh token security.
- OAuth state validation.
- Specific CORS.
- Rate limiting.
- Input validation.
- File upload validation.
- MIME/type validation.
- File size limits.
- ORM/parameterized query.
- XSS protection.
- Admin audit logging.
- Không commit secrets vào Git.

AI:
- Per-user rate limit.
- Usage monitoring.
- Không lưu dữ liệu nhạy cảm không cần thiết.

---

# 34. Non-functional requirements

## Performance
- Lazy loading route.
- Pagination.
- Server-side filtering.
- Cache dữ liệu ít thay đổi.
- Optimize media delivery.

## Reliability
- Global exception handling.
- AI retry ở mức an toàn.
- Timeout.
- Structured logging.
- Health checks.

## Scalability
Backend stateless để có thể scale nhiều instance.

## Maintainability
- DTO.
- Service layer.
- Repository khi thực sự cần.
- Unit tests cho business logic.
- Integration tests cho API quan trọng.

---

# 35. MVP vs Phase 2 vs Phase 3

## MVP — bắt buộc
1. Authentication.
2. Student/Teacher/Admin.
3. Course/Module/Lesson.
4. Exercise Engine.
5. Question Bank.
6. Listening.
7. Reading.
8. Writing cơ bản.
9. Speaking cơ bản.
10. Placement Test.
11. Mock Test.
12. Dashboard.
13. Progress.
14. AI Tutor.
15. Gemini Writing evaluation.
16. Basic Speaking evaluation.
17. Teacher class.
18. Teacher review.
19. Admin Dashboard.
20. Vercel + Render + Neon deployment.

## Phase 2
1. AI adaptive learning nâng cao.
2. AI-generated course content.
3. Advanced gamification.
4. Leaderboard.
5. Advanced analytics.
6. Calendar reminders.
7. Rich notifications.
8. Media optimization.
9. Advanced speech analysis.
10. Personalized mock generation.

## Phase 3
1. Real-time speaking conversation.
2. Streaming speech.
3. Deep AI conversation memory.
4. Advanced teacher analytics.
5. Recommendation engine.
6. Mobile app.
7. Multi-provider AI fallback.

---

# 36. Recommended Development Order

## Stage 1 — Foundation
```text
Solution setup
→ PostgreSQL/Neon
→ ASP.NET Identity
→ JWT/Auth
→ Google/GitHub OAuth
→ React routing/layout
```

## Stage 2 — Learning Core
```text
Course
→ Module
→ Lesson
→ Question
→ Exercise
→ Result
→ Explanation
```

## Stage 3 — IELTS Skills
```text
Listening
Reading
Writing
Speaking
```

## Stage 4 — Assessment
```text
Placement Test
→ Mock Test
→ Exam Mode
→ Results
→ Progress
```

## Stage 5 — AI
```text
AI Tutor
→ Explanation
→ Writing Evaluation
→ Speaking Evaluation
→ Recommendation
```

## Stage 6 — Teacher/Admin
```text
Class
→ Assignment
→ Teacher Review
→ Admin Dashboard
```

## Stage 7 — Gamification & Growth
```text
XP
→ Streak
→ Achievement
→ Leaderboard
→ Notifications
→ Calendar
```

## Stage 8 — Deployment
```text
GitHub
→ Vercel
→ Render
→ Neon
→ Object Storage
→ Production
```

---

# 37. Recommended Initial ERD Scope

Phiên bản đầu tiên ưu tiên:

```text
AspNetUsers
AspNetRoles
RefreshTokens

Levels
Courses
Modules
Lessons
LessonSections

Exercises
Questions
QuestionOptions
QuestionTags

PlacementTests
PlacementAttempts
MockTests
MockTestSections
MockTestQuestions
TestAttempts
TestAnswers

WritingSubmissions
WritingEvaluations
SpeakingSessions
SpeakingEvaluations

UserProgress
QuestionAttempts
StudySessions
StudyPlans

Classes
ClassMembers
Assignments
AssignmentSubmissions
TeacherReviews

AIAssistantSessions
AIMessages
AIUsageLogs

XPTransactions
Achievements
UserAchievements
Streaks

Notifications
Bookmarks
Favorites
CalendarEvents
AuditLogs
MediaAssets
```

---

# 38. Decision Log

| Chủ đề | Quyết định |
|---|---|
| Đối tượng | Tất cả trình độ |
| Level | Basic → Advanced |
| Skills | Listening, Reading, Writing, Speaking + Grammar/Vocabulary/Pronunciation |
| Platform | IELTS online learning platform hoàn chỉnh |
| AI | Trợ giảng chính |
| AI Provider | Google Gemini |
| AI Language | Việt + English |
| Account | Email + Google + GitHub |
| Auth | ASP.NET Core Identity + JWT + Refresh Token |
| Roles | Student / Teacher / Admin |
| Payment | Chưa triển khai |
| Mock Test | Practice + Exam Mode |
| Placement Test | Có |
| Progress | Có đầy đủ |
| Gamification | Có |
| Search | Có |
| Notifications | Có |
| Calendar | Có |
| Bookmark/Favorite | Có |
| Notes | Không |
| Dark Mode | Không |
| Backend | ASP.NET Core Web API |
| Frontend | React |
| Database | PostgreSQL |
| DB Hosting | Neon |
| Backend Hosting | Render |
| Frontend Hosting | Vercel |
| AI | Gemini |
| File storage | Object Storage |

---

# 39. Product Principle

Vòng lặp cốt lõi:

> **Learn → Practice → Evaluate → Understand Mistakes → Ask AI → Improve → Retest**

AI không chỉ trả lời câu hỏi. AI phải giúp người học hiểu:
1. Tại sao sai.
2. Cần cải thiện gì.
3. Nên học gì tiếp theo.
4. Làm thế nào để tiến đến target band.

---

# 40. Scope Note

Đây là scope lớn. Để hoàn thành và deploy ổn định, phải triển khai theo **MVP → Phase 2 → Phase 3** thay vì xây toàn bộ AI, Speaking realtime, analytics và gamification nâng cao ngay từ đầu.

Lõi sản phẩm cần chứng minh được:

```text
Student
→ Learning Content
→ Practice
→ Score
→ Progress
→ AI Feedback
→ Recommended Next Lesson
```
