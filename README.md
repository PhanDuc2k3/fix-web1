# fix-web1

## 🌐 Domain Configuration

### Backend API (Render)
- **Production URL**: `https://fix-web1.onrender.com`
- **API Base URL**: `https://fix-web1.onrender.com/api`

### Frontend (Vercel)
- **Production URL**: `https://fix-web1.vercel.app`

## 📝 Những điểm cần thay đổi khi đổi domain

### 1. Backend - CORS Configuration
**File**: `backend/server.js`

Nếu bạn muốn thêm hoặc thay đổi domain frontend được phép truy cập API, cần cập nhật trong phần CORS:

```javascript
// CORS Configuration
const allowedOrigins = [
  'https://fix-web1.vercel.app',      // Frontend Vercel
  'https://fix-web1.onrender.com',    // Frontend Render (nếu có)
  'https://deploy-livid-omega.vercel.app', // Frontend backup
  // Có thể thêm domain khác tại đây
];
```

**Vị trí**: Dòng 69-77 trong `backend/server.js`

### 2. Frontend - API Base URL
**File**: `frontend/src/utils/api.js`

Để thay đổi domain backend API, cần cập nhật:

```javascript
const API_URL = import.meta.env.VITE_API_URL || 'https://fix-web1.onrender.com/api';
```

**Vị trí**: Dòng 3 trong `frontend/src/utils/api.js`

**Lưu ý**: 
- Có thể sử dụng biến môi trường `VITE_API_URL` để override
- Tạo file `.env` trong thư mục `frontend` với nội dung: `VITE_API_URL=https://your-backend-url.com/api`

### 3. Environment Variables

#### Backend `.env`
Tạo file `.env` trong thư mục `backend` hoặc root:

```env
MONGO_URI=your_mongodb_connection_string
EMAIL_USER=your_email@gmail.com
EMAIL_PASSWORD=your_app_password
CLIENT_URL=https://fix-web1.vercel.app,https://fix-web1.onrender.com
PORT=5000
```

#### Frontend `.env`
Tạo file `.env` trong thư mục `frontend`:

```env
VITE_API_URL=https://fix-web1.onrender.com/api
```

## 🚀 Deployment

### Backend (Render)
1. Đảm bảo domain backend là: `https://fix-web1.onrender.com`
2. Cấu hình CORS trong `backend/server.js` đã bao gồm domain frontend
3. Set environment variables trên Render dashboard

### Frontend (Vercel)
1. Đảm bảo domain frontend là: `https://fix-web1.vercel.app`
2. API calls sẽ tự động sử dụng domain từ `frontend/src/utils/api.js`
3. Có thể override bằng environment variable `VITE_API_URL` trên Vercel

## ✅ Checklist khi đổi domain

- [ ] Cập nhật `allowedOrigins` trong `backend/server.js` (dòng 69-77)
- [ ] Cập nhật `API_URL` trong `frontend/src/utils/api.js` (dòng 3)
- [ ] Cập nhật environment variables trên Render (nếu có `CLIENT_URL`)
- [ ] Cập nhật environment variables trên Vercel (nếu có `VITE_API_URL`)
- [ ] Test API connection từ frontend mới
- [ ] Kiểm tra CORS không bị chặn

## 🔍 Kiểm tra domain hiện tại

### Backend CORS
Xem trong `backend/server.js` tại dòng 69-77

### Frontend API
Xem trong `frontend/src/utils/api.js` tại dòng 3

## 📞 Support

Nếu gặp lỗi CORS, kiểm tra:
1. Domain frontend có trong `allowedOrigins` của backend không
2. Domain backend có đúng trong `frontend/src/utils/api.js` không
3. Environment variables đã được set đúng chưa
