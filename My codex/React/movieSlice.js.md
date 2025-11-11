```JavaScript
import { createSlice, createAsyncThunk } from "@reduxjs/toolkit";
import api from "services/apiService"; // Adjust path as needed

const initialState = {
  detail: {
    loading: false,
    data: null,
    error: null,
  },
  reviews: {
    loading: false,
    data: null,
    error: null,
  },
};

export const fetchMovieDetail = createAsyncThunk(
  "movie/fetchDetail",
  async (id, { rejectWithValue }) => {
    try {
      const response = await api.get(`QuanLyPhim/LayThongTinPhim?MaPhim=${id}`);
      return response.data.content;
    } catch (error) {
      return rejectWithValue(error.response?.data || error.message);
    }
  }
);

export const fetchMovieReviews = createAsyncThunk(
  "movie/fetchReviews",
  async (id, { rejectWithValue }) => {
    try {
      const response = await api.get(`QuanLyPhim/LayDanhGiaPhim?MaPhim=${id}`);
      return response.data.content;
    } catch (error) {
      return rejectWithValue(error.response?.data || error.message);
    }
  }
);

const movieSlice = createSlice({
  name: "movie",
  initialState,
  reducers: {},
  extraReducers: (builder) => {
    builder
      .addCase(fetchMovieDetail.pending, (state) => {
        state.detail.loading = true;
        state.detail.error = null;
      })
      .addCase(fetchMovieDetail.fulfilled, (state, action) => {
        state.detail.loading = false;
        state.detail.data = action.payload;
      })
      .addCase(fetchMovieDetail.rejected, (state, action) => {
        state.detail.loading = false;
        state.detail.error = action.payload;
      })
      .addCase(fetchMovieReviews.pending, (state) => {
        state.reviews.loading = true;
        state.reviews.error = null;
      })
      .addCase(fetchMovieReviews.fulfilled, (state, action) => {
        state.reviews.loading = false;
        state.reviews.data = action.payload;
      })
      .addCase(fetchMovieReviews.rejected, (state, action) => {
        state.reviews.loading = false;
        state.reviews.error = action.payload;
      });
  },
});

export default movieSlice.reducer;
```

Chú thích:
![[Pasted image 20251111214912.png]]

#typePrefix để phân biệt các Thunk giữa các module
```JavaScript
// Trong module1.js
export const fetchMovieDetail = createAsyncThunk(/* ... */);

// Trong module2.js
export const fetchMovieDetail = createAsyncThunk(/* ... */);

// Trong index.jsx
import { fetchMovieDetail as fetchDetailFromModule1 } from './module1';
import { fetchMovieDetail as fetchDetailFromModule2 } from './module2';

// Dispatch
dispatch(fetchDetailFromModule1(id));
```

#rejectWithValue 
là hàm trả về error.response?.data || error.message và state error là action.payload của rejected case, để state.error nhận giá trị chi tiết đó.

