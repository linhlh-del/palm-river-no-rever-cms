# Palm River CMS (không Rever)

CMS riêng cho `palm-river-no-rever`, dựa trên giao diện và quyền của `norton-park-cms` / `sensa-park-cms`.

## Chạy thử tại máy

```bash
npm ci
npm run dev
```

Tạo `.env.local` với `VITE_CMS_DEMO=1` (hoặc chép từ `.env.example`): đăng nhập demo, bản nháp lưu ở localStorage, schema đọc từ `public/cms-schema.json`, cổng 5183. Demo không đăng lên website và không có lead/analytics thật.

## Kết nối production

Đặt trong Vercel của CMS: `VITE_SUPABASE_URL`, `VITE_SUPABASE_ANON_KEY`, `VITE_SITE_URL=https://canho-palmriver.com.vn`. Bỏ `VITE_CMS_DEMO` trên production. CMS đọc `VITE_SITE_URL/cms-schema.json` và `/cms-status.json`.

Backend dùng chung trong `../cms-supabase`: chạy migration `20261102000000_palm_river_projects.sql`, thêm owner vào `cms_members` với `project_id='palm-river-no-rever'`, deploy lại `cms-admin` và `collect`. Thêm origin CMS vào `CMS_ORIGINS` và tạo secret `DEPLOY_HOOK_PALM_RIVER_NO_REVER`. Có thể thêm `VERCEL_PROJECT_ID_PALM_RIVER_NO_REVER` để xem trạng thái deploy.

Landing page cần `CMS_SUPABASE_URL`, `CMS_SUPABASE_ANON_KEY`, `VITE_CMS_COLLECT_URL` và `CMS_SITE_URL`; xem `../palm-river-no-rever/CMS.md`. Mục Lead chỉ có dữ liệu khi Worker lead hiện tại ghi thêm bản sao vào `public.cms_leads` với đúng `project_id`. Không đưa service role key vào CMS hay landing page.
