# Hướng dẫn push GitHub — link THẬT của bạn

> Claude Desktop không đăng nhập GitHub được → phần này để **Cursor / Claude Code chạy trên máy bạn**.
> 2 repo:
> - APP code (PRIVATE): `https://github.com/Tamthanhaugustino/TamMetaDev.git`
> - POLICY (PUBLIC): `https://github.com/Tamthanhaugustino/app-policies.git`

---
## A. Repo POLICY (PUBLIC) — `app-policies`
Folder: `C:\Vibe Code\Du An Code App Amazon\app-policies`
```
cd "C:\Vibe Code\Du An Code App Amazon\app-policies"
git init
git add .
git commit -m "Add app privacy policies"
git branch -M main
git remote add origin https://github.com/Tamthanhaugustino/app-policies.git
git push -u origin main
```
Bật Pages: GitHub → repo `app-policies` → **Settings → Pages → Source = main / (root) → Save**.

→ Sau ~1 phút có link (chữ thường):
**`https://tamthanhaugustino.github.io/app-policies/trivia-quiz.html`**
Đây là **Privacy Policy URL** để dán khi nộp #31. (Nếu 404, kiểm tra hoa/thường của username.)

---
## B. Repo APP CODE (PRIVATE) — `TamMetaDev`  [monorepo cả dự án]
Đưa nguyên thư mục dự án (engines + 100 app + Quiz31) lên 1 repo private để backup + quản lý.
Folder gốc repo: `C:\Vibe Code\Du An Code App Amazon\100 App Amazon`

⚠️ Đã có sẵn `.gitignore` (mình vừa bổ sung) chặn: `*.keystore`, `*.jks`, `local.properties`, `node_modules`, các thư mục build, `*.apk/.aab`. **Kiểm tra lại trước khi commit.**

```
cd "C:\Vibe Code\Du An Code App Amazon\100 App Amazon"
git init
git add .
git commit -m "100 app Amazon - source (engines + apps + Quiz31 pilot)"
git branch -M main
git remote add origin https://github.com/Tamthanhaugustino/TamMetaDev.git
git push -u origin main
```

⚠️ Nếu trong `031 - General Knowledge Quiz\Quiz31` đã có `.git` riêng (do init lúc build) → sẽ thành nested repo/submodule. Xử lý: hoặc xoá `Quiz31\.git` để gộp chung, hoặc push Quiz31 thành repo riêng. Bảo Claude Code quyết.

KIỂM TRA KHÔNG LỌT SECRET (chạy sau commit):
```
git ls-files | findstr /I "keystore jks local.properties"
```
→ **Phải KHÔNG ra dòng nào.** Nếu có → `git rm --cached <file>` rồi commit lại.

---
## PROMPT dán cho Claude Code trong Cursor
```
Push 2 repo (gh/git đã đăng nhập sẵn):

1) POLICY public: cd "C:\Vibe Code\Du An Code App Amazon\app-policies" -> git init, add, commit, branch -M main, remote add origin https://github.com/Tamthanhaugustino/app-policies.git, push -u origin main. Rồi hướng dẫn tôi bật GitHub Pages (main/root). Báo URL trivia-quiz.html.

2) APP private (monorepo): cd "C:\Vibe Code\Du An Code App Amazon\100 App Amazon". Kiểm tra .gitignore đã chặn *.keystore, *.jks, local.properties, node_modules, build, *.apk/.aab. Nếu Quiz31 có .git lồng thì xoá Quiz31\.git để gộp chung. git init, add, commit, branch -M main, remote add origin https://github.com/Tamthanhaugustino/TamMetaDev.git, push -u origin main.
Cuối cùng chạy: git ls-files | findstr /I "keystore jks local.properties"  -> xác nhận KHÔNG có secret nào bị commit. Báo kết quả.
```
