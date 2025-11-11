// HÀM TẠO API CLIENT
HÀM createApi(storageKey):
    // 1. KHỞI TẠO AXIOS INSTANCE
    api = axios.create với baseURL
    
    // 2. INTERCEPTOR CHO REQUEST
    api.interceptors.request.use(
        KHI_THÀNH_CÔNG(config):
            // Lấy thông tin user từ localStorage
            userInfo = localStorage.getItem(storageKey)
            accessToken = ""
            
            NẾU userInfo tồn tại:
                THỬ:
                    accessToken = "Bearer " + JSON.parse(userInfo).accessToken
                BẮT_LỖI:
                    ghi log lỗi
            
            // Thiết lập headers
            config.headers = {
                ...headers cũ,
                Authorization: accessToken,
                TokenCybersoft: token từ env hoặc default
            }
            
            TRẢ_VỀ config
            
        KHI_LỖI(error):
            TRẢ_VỀ Promise.reject(error)
    )
    
    // 3. INTERCEPTOR CHO RESPONSE
    api.interceptors.response.use(
        KHI_THÀNH_CÔNG(response):
            TRẢ_VỀ response
            
        KHI_LỖI(error):
            originalRequest = error.config
            
            // Xử lý lỗi 401 (Unauthorized)
            NẾU error.status = 401 VÀ originalRequest chưa retry:
                originalRequest._retry = true
                
                THỬ:
                    // Lấy refresh token
                    userInfo = JSON.parse(localStorage.getItem(storageKey) hoặc "{}")
                    refreshToken = userInfo.refreshToken
                    
                    // Gọi API refresh token
                    refreshResponse = GỬI_POST("/refresh-token", {refreshToken})
                    
                    // Cập nhật access token mới
                    newAccessToken = refreshResponse.data.accessToken
                    
                    // Lưu token mới vào localStorage
                    localStorage.setItem(storageKey, JSON.stringify({
                        ...userInfo cũ,
                        accessToken: newAccessToken
                    }))
                    
                    // Thử lại request gốc
                    originalRequest.headers.Authorization = "Bearer " + newAccessToken
                    TRẢ_VỀ api(originalRequest)
                    
                BẮT_LỖI refreshError:
                    // Refresh thất bại - đăng xuất
                    ghi log lỗi
                    xóa storageKey khỏi localStorage
                    chuyển hướng đến trang login
                    TRẢ_VỀ Promise.reject(refreshError)
            
            // Với các lỗi khác
            TRẢ_VỀ Promise.reject(error)
    )
    
    TRẢ_VỀ api

// TẠO CÁC INSTANCE CỤ THỂ
apiAdmin = createApi("ADMIN_INFO")
apiUser = createApi("USER_INFO")

```JavaScript
import axios from "axios";
const createApi = (storageKey) => {
  const api = axios.create({
    baseURL: "https://movienew.cybersoft.edu.vn/api/",
  });
  api.interceptors.request.use(
    (config) => {
      const userInfo = localStorage.getItem(storageKey);
      let accessToken = "";
      if (userInfo) {
        try {
          accessToken = "Bearer " + JSON.parse(userInfo).accessToken;
        } catch (e) {
          console.error(`Invalid ${storageKey}`, e);
        }
      }
      config.headers = {
        ...config.headers,
        Authorization: accessToken,
        TokenCybersoft:
          process.env.REACT_APP_TOKEN_CYBERSOFT ||
          "your-default-token",
      };
      return config;
    },
    (error) => Promise.reject(error)
  );
  api.interceptors.response.use(
    (response) => response,
    async (error) => {
      const originalRequest = error.config;
      if (error.response?.status === 401 && !originalRequest._retry) {
        originalRequest._retry = true;
        try {
          const userInfo = JSON.parse(
            localStorage.getItem(storageKey) || "{}"
          );
          const refreshToken = userInfo.refreshToken || "";
          const refreshResponse = await api.post("/refresh-token", {
            refreshToken,
          });
          const newAccessToken = refreshResponse.data.accessToken;
          localStorage.setItem(
            storageKey,
            JSON.stringify({
              ...userInfo,
              accessToken: newAccessToken,
            })
          );
          originalRequest.headers.Authorization =
            "Bearer " + newAccessToken;
          return api(originalRequest);
        } catch (refreshError) {
          console.error("Refresh token failed", refreshError);
          localStorage.removeItem(storageKey);
          window.location.href = "/login";
          return Promise.reject(refreshError);
        }
      }
      return Promise.reject(error);
    }
  );
  return api;
};
export const apiAdmin = createApi("ADMIN_INFO");
export const apiUser = createApi("USER_INFO");
```