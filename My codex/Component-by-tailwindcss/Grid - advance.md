### **1. CONTAINER

```jsx
{/*  Container với breakpoints và max-width hợp lý */}
<div className="container mx-auto px-4 sm:px-6 lg:px-8 max-w-7xl">
  {/* Content */}
</div>

{/* 🎯 Tại sao: 
- px-4 sm:px-6 lg:px-8: Padding responsive
- max-w-7xl: Ngăn container quá rộng trên màn hình lớn
*/}
```

### **2. GRID SYSTEM NÂNG CAO**

markdown

```jsx
{/*  Grid với gap responsive và fallback */}
<div className="grid grid-cols-1 xs:grid-cols-2 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 2xl:grid-cols-6 gap-4 sm:gap-6 md:gap-8">
  {renderCards()}
</div>

{/* 🎯 Tại sao:
- xs:grid-cols-2: Breakpoint tùy chỉnh cho mobile nhỏ
	- gap responsive: gap-4 (mobile) → gap-8 (desktop)
- Column count tăng dần theo breakpoint
- 2xl ở grid dù max-w ở container là xl do áp dụng CSS CASCADE & INHERITANCE
*/}
```
### **3. CARD WRAPPER VỚI LOADING & EMPTY STATES**

markdown

```jsx
{/* ✅ Grid với các states */}
<div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
  {/* Loading State */}
  {isLoading && (
    Array.from({ length: 8 }).map((_, index) => (
      <CardSkeleton key={index} />
    ))
  )}
  
  {/* Empty State */}
  {!isLoading && cards.length === 0 && (
    <div className="col-span-full text-center py-12">
      <EmptyState />
    </div>
  )}
  
  {/* Data State */}
  {!isLoading && cards.map(card => (
    <Card key={card.id} {...card} />
  ))}
</div>
```
### **4. AUTO-FIT GRID (FLEXIBLE)**

markdown

```html
<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Auto-fit Grid Demo</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    /* ✅ Auto-fit áp dụng ngay từ đầu, không phụ thuộc breakpoint */
    .grid-cols-auto-fit {
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    }
  </style>
</head>
<body class="bg-gray-100 p-8">

  <h2 class="text-xl font-semibold mb-4 text-green-600">
    ✅ Auto-fit grid: số cột thay đổi thực sự theo viewport
  </h2>

  <div class="grid grid-cols-auto-fit gap-6">
    <div class="bg-green-200 p-6 rounded-xl text-center font-semibold">Card 1</div>
    <div class="bg-green-300 p-6 rounded-xl text-center font-semibold">Card 2</div>
    <div class="bg-green-400 p-6 rounded-xl text-center font-semibold">Card 3</div>
    <div class="bg-green-500 p-6 rounded-xl text-center font-semibold">Card 4</div>
    <div class="bg-green-600 p-6 rounded-xl text-center font-semibold">Card 5</div>
    <div class="bg-green-700 p-6 rounded-xl text-center font-semibold">Card 6</div>
    <div class="bg-green-800 p-6 rounded-xl text-center font-semibold">Card 7</div>
    <div class="bg-green-900 p-6 rounded-xl text-center font-semibold">Card 8</div>
  </div>

</body>
</html>

```

### **5. GRID VỚI FEATURES NÂNG CAO**

markdown

```jsx
{/* ✅ Grid với masonry layout và hover effects */}
<div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6 auto-rows-min">
  {cards.map((card, index) => (
    <div 
      key={card.id}
      className={`
        bg-white rounded-xl shadow-sm border border-gray-100 
        hover:shadow-lg hover:border-blue-200 transition-all 
        duration-300 transform hover:-translate-y-1
        ${index === 0 ? 'sm:col-span-2 sm:row-span-2' : ''}
        ${card.featured ? 'lg:col-span-2' : ''}
      `}
    >
      <CardContent {...card} />
    </div>
  ))}
</div>
```

## 📋 **CHECKLIST ĐẦY ĐỦ:**

markdown

# ✅ GRID CHECKLIST "ĐI LÀM"

## 🏗 Container Level
- [ ] Container với padding responsive
- [ ] Max-width phù hợp
- [ ] Margin auto cho center

## 📱 Grid Layout  
- [ ] Breakpoints từ mobile → desktop
- [ ] Gap responsive
- [ ] Column count hợp lý
- [ ] Auto-rows cho chiều cao

## 🎨 UX/UI
- [ ] Loading states
- [ ] Empty states  
- [ ] Error states
- [ ] Hover effects
- [ ] Transition animations

## ⚡ Performance
- [ ] Key props unique
- [ ] Lazy loading cho ảnh
- [ ] Virtual scroll nếu nhiều items
- [ ] Memoization nếu cần

## 🎯 Advanced Features
- [ ] Masonry layout (nếu cần)
- [ ] Featured items span columns
- [ ] Dynamic grid templates
- [ ] Custom breakpoints