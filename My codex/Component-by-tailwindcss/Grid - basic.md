Tạo container chứa grid
```html
<div className=" container mx-auto p-4"> 
</div>
```
Tạo grid
 ```html
 <div className="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4">
          {renderCard()}
  </div>
```
Thêm style cho card:
- bg-white: Nền trắng.
- rounded-lg: Bo góc.
- shadow-md: Bóng nhẹ.
- overflow-hidden: Tránh nội dung tràn ra.
- w-full h-48 object-cover: Hình ảnh full width, crop để fit.
- p-4: Padding cho nội dung.
- text-lg font-semibold: Style cho tiêu đề.
- hover:bg-blue-600: Hover effect cho button.