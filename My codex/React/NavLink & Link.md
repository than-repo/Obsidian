NavLink:
Link

ROUTER
```JavaScript
const router = createBrowserRouter([
  {
    element: <Layout />,
    children: [
      // NHÁNH 1
      { 
        path: "Lv1",
        element: <Lv1Page />,
        children: [
          { path: "Lv2", element: <Lv2Page /> },
          { 
            path: "Lv2/Lv3", 
            element: <Lv3Page /> 
          }
        ]
      },
      // NHÁNH 2  
      { 
        path: "A",
        element: <APage />,
        children: [
          { path: "B", element: <BPage /> },
          { 
            path: "B/C", 
            element: <CPage /> 
          }
        ]
      }
    ]
  }
]);

//router.js
**Khác nhánh**
import { NavLink } from 'react-router-dom';

const NavigationComponent = () => {
  return (
    <nav>
      {/* DI CHUYỂN GIỮA 2 NHÁNH - DÙNG ABSOLUTE PATHS */}
      
      {/* Từ Nhánh 1 sang Nhánh 2 */}
      <NavLink to="/A" className={({ isActive }) => isActive ? "active" : ""}>
        Từ Lv1/Lv2/Lv3 → Sang A
      </NavLink>
      
      <NavLink to="/A/B" className={({ isActive }) => isActive ? "active" : ""}>
        Từ Lv1/Lv2/Lv3 → Sang B
      </NavLink>

      <NavLink to="/A/B/C" className={({ isActive }) => isActive ? "active" : ""}>
        Từ Lv1/Lv2/Lv3 → Sang C
      </NavLink>

      {/* Từ Nhánh 2 sang Nhánh 1 */}
      <NavLink to="/Lv1" className={({ isActive }) => isActive ? "active" : ""}>
        Từ A/B/C → Sang Lv1
      </NavLink>

      <NavLink to="/Lv1/Lv2" className={({ isActive }) => isActive ? "active" : ""}>
        Từ A/B/C → Sang Lv2
      </NavLink>

      <NavLink to="/Lv1/Lv2/Lv3" className={({ isActive }) => isActive ? "active" : ""}>
        Từ A/B/C → Sang Lv3
      </NavLink>

      {/* NAVIGATION TRONG CÙNG NHÁNH - DÙNG RELATIVE */}
      <NavLink to="../" className={({ isActive }) => isActive ? "active" : ""}>
        Lùi 1 cấp (relative)
      </NavLink>

      <NavLink to="child" className={({ isActive }) => isActive ? "active" : ""}>
        Tới con trực tiếp (relative)
      </NavLink>
    </nav>
  );
};

**Cùng nhánh**
import { useNavigate } from "react-router-dom";
const Component = () => {
  const navigate = useNavigate();
  // Đi lùi (backward) n cấp: dùng đường dẫn relative
  const goBackToParent = () => navigate("../"); // Lùi 1 cấp
  const goBackMultiple = () => navigate("../../"); // Lùi 2 cấp (ví dụ từ Lv4 về Lv2)
  // Đi tới (forward) nested con: dùng đường dẫn relative hoặc absolute
  const goForwardChild = () => navigate("child"); // Tới con trực tiếp
  const goForwardDeep = () => navigate("child/grandchild"); // Tới con cháu
  const goAbsolute = () => navigate("/absolute/path"); // Đường dẫn tuyệt đối
  return (
    <>
      <button onClick={goBackToParent}>Lùi 1 cấp</button>
      <button onClick={goBackMultiple}>Lùi 2 cấp</button>
      <button onClick={goForwardChild}>Tới con</button>
      <button onClick={goForwardDeep}>Tới con cháu</button>
      <button onClick={goAbsolute}>Tới absolute</button>
    </>
  );
};
## **GIẢI THÍCH:**

- `./` = **current directory** (ở ngay đây)
    
- `../` = **parent directory** (lùi 1 cấp)
    
- `../../` = **parent of parent** (lùi 2 cấp)
```

