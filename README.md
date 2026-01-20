# ACM-x-ACMW-React-Fullstack-Mini-Series

React Counter & History Demo

A simple React workshop project demonstrating components, state, and routing.
Participants will build a counter that tracks history and uses routing to show different views.

Prerequisites

Node.js installed (Download here
)

Basic familiarity with terminal commands

Verify installation:

node -v
npm -v

Step 1: Create the Project

Open terminal and navigate to the folder where you want to create the project:

pwd


Run Vite’s project creation command:

npm create vite@latest


Follow the prompts:

Project name: your choice

Package name: your choice

Framework: React

Variant: JavaScript

Rollup TypeScript: No

Install dependencies now: Yes

Start the development server:

npm run dev


Copy the local URL from the terminal (e.g., http://localhost:5173) into your browser. You should see the Vite React starter page.

Step 2: Prepare Your Project

Delete index.css (we’ll use inline styles for simplicity)

Remove the import of index.css in main.jsx:

- import './index.css';


In the src folder, create a new file called Counter.jsx.

Step 3: Create the Counter Component

In Counter.jsx, we define the main component that will handle:

The counter value

Increment and decrement logic

History tracking

Conditional rendering depending on which page is displayed

Counter.jsx
import { useState } from "react";

// Counter component receives props to control its behavior
export default function Counter({ showHistory = false, showControls = true }) {
  // State to keep track of the current count
  const [count, setCount] = useState(0);
  // State to keep track of the history of counts
  const [history, setHistory] = useState([]);

  // Increment function
  const increment = () => {
    const next = count + 1;
    setCount(next);
    setHistory([...history, next]); // store the new value in history
  };

  // Decrement function
  const decrement = () => {
    const next = count - 1;
    setCount(next);
    setHistory([...history, next]); // store the new value in history
  };

  // Inline styles for simplicity
  const styles = {
    container: {
      height: "100vh",
      display: "flex",
      flexDirection: "column",
      justifyContent: "center",
      alignItems: "center",
      gap: "16px",
      fontFamily: "Arial, sans-serif",
      backgroundColor: "#f5f5f5",
    },
    buttons: {
      display: "flex",
      gap: "10px",
    },
    button: {
      padding: "10px 16px",
      fontSize: "16px",
      borderRadius: "6px",
      border: "1px solid #ccc",
      cursor: "pointer",
      backgroundColor: "white",
    },
    history: {
      fontSize: "16px",
      maxWidth: "300px",
      textAlign: "center",
      color: "#555",
    },
  };

  return (
    <div style={styles.container}>
      {/* Title */}
      <h1>Click Counter</h1>

      {/* Current counter value */}
      <h2>{count}</h2>

      {/* Buttons (conditionally rendered based on showControls prop) */}
      {showControls && (
        <div style={styles.buttons}>
          <button style={styles.button} onClick={decrement}>-1</button>
          <button style={styles.button} onClick={increment}>+1</button>
        </div>
      )}

      {/* History (conditionally rendered based on showHistory prop) */}
      {showHistory && (
        <p style={styles.history}>
          {history.join(" → ") || "No clicks yet"}
        </p>
      )}
    </div>
  );
}


Explanation for beginners:

useState keeps track of counter and history

showControls and showHistory props allow reusing the component on different pages

Buttons update state, and history is displayed if showHistory is true

Step 4: Set Up Routing in App.jsx

Now we’ll use React Router to display different views:

/ → Counter with buttons

/history → Counter history only

App.jsx
import { BrowserRouter, Routes, Route, Link } from "react-router-dom";
import Counter from "./Counter";

export default function App() {
  // Style for the navigation links
  const linkStyle = {
    position: "fixed",
    bottom: "20px",
    textDecoration: "none",
    fontWeight: "bold",
  };

  return (
    <BrowserRouter>
      <Routes>
        {/* Home page: counter + buttons */}
        <Route
          path="/"
          element={
            <>
              <Counter showHistory={false} showControls={true} />
              <Link to="/history" style={linkStyle}>View History →</Link>
            </>
          }
        />

        {/* History page: counter + history only */}
        <Route
          path="/history"
          element={
            <>
              <Counter showHistory={true} showControls={false} />
              <Link to="/" style={linkStyle}>← Back</Link>
            </>
          }
        />
      </Routes>
    </BrowserRouter>
  );
}


Explanation for beginners:

BrowserRouter wraps the app to enable routing

<Routes> contains all possible routes

<Route path="/" element={...}> defines what renders at /

<Link> updates the URL without refreshing the page

Step 5: Run and Test

Start the development server:

npm run dev


Open the URL in your browser

On /, click the buttons — the counter should increase or decrease

Click View History → to go to /history — the buttons disappear, and you see all previous values

Click ← Back to return to the counter

Step 6: Recap & Key Takeaways

Components can be reused with props to show different UI

State can be shared inside a component and passed through routes

React Router allows single-page navigation

Inline styling is simple and works for small demos
