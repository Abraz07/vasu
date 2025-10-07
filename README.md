Here’s a **simple and clear React Routing POC** for your requirement —
three components: **StartComp → RectComp → ResultComp**.
It uses **React Router v6**.

---

### 🧩 Folder structure

```
src/
 ├── App.js
 ├── StartComp.js
 ├── RectComp.js
 └── ResultComp.js
```

---

### 1️⃣ App.js

```jsx
import { BrowserRouter as Router, Routes, Route } from "react-router-dom";
import StartComp from "./StartComp";
import RectComp from "./RectComp";
import ResultComp from "./ResultComp";

export default function App() {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<StartComp />} />
        <Route path="/rectangle" element={<RectComp />} />
        <Route path="/result" element={<ResultComp />} />
      </Routes>
    </Router>
  );
}
```

---

### 2️⃣ StartComp.js

```jsx
import { Link } from "react-router-dom";

export default function StartComp() {
  return (
    <div style={{ textAlign: "center", marginTop: "50px" }}>
      <h2>Welcome to Rectangle Calculator</h2>
      <Link to="/rectangle">Go to Rectangle Component</Link>
    </div>
  );
}
```

---

### 3️⃣ RectComp.js

```jsx
import { useState } from "react";
import { useNavigate } from "react-router-dom";

export default function RectComp() {
  const [length, setLength] = useState("");
  const [breadth, setBreadth] = useState("");
  const navigate = useNavigate();

  const handleSubmit = () => {
    if (!length || !breadth) {
      alert("Please enter both values");
      return;
    }

    const area = length * breadth;
    const perimeter = 2 * (Number(length) + Number(breadth));

    navigate("/result", { state: { area, perimeter } });
  };

  return (
    <div style={{ textAlign: "center", marginTop: "50px" }}>
      <h2>Rectangle Calculator</h2>
      <input
        type="number"
        placeholder="Enter Length"
        value={length}
        onChange={(e) => setLength(e.target.value)}
      />
      <br /><br />
      <input
        type="number"
        placeholder="Enter Breadth"
        value={breadth}
        onChange={(e) => setBreadth(e.target.value)}
      />
      <br /><br />
      <button onClick={handleSubmit}>Calculate</button>
    </div>
  );
}
```

---

### 4️⃣ ResultComp.js

```jsx
import { useLocation, Link } from "react-router-dom";

export default function ResultComp() {
  const location = useLocation();
  const { area, perimeter } = location.state || {};

  return (
    <div style={{ textAlign: "center", marginTop: "50px" }}>
      <h2>Result</h2>
      {area !== undefined ? (
        <>
          <p>Area: {area}</p>
          <p>Perimeter: {perimeter}</p>
        </>
      ) : (
        <p>No data found. Go back to input values.</p>
      )}
      <Link to="/rectangle">Back</Link>
    </div>
  );
}
```

---

### ⚡ How it works

1. **StartComp** → Shows a link → `/rectangle`
2. **RectComp** → Two textboxes (length & breadth) + Button
   → On click → navigates to `/result` and passes computed values.
3. **ResultComp** → Displays **Area** and **Perimeter**.

---

Would you like me to make it look a bit stylish (centered card, neat input boxes, button style) using Tailwind or plain CSS?
