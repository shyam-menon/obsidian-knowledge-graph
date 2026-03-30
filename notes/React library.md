### **Notes**

- **React 19 (The UI Library):**
    
    - **Declarative UI:** You describe _what_ the UI should look like for a given state, and React handles the DOM updates.
    
    - **Component-Based:** Logic and UI are encapsulated into reusable "bricks" (Components).
    
    - **The Compiler Shift:** React 19 introduces a compiler that automatically optimizes re-renders, removing the need for manual `useMemo`.
        
- **Vite 8 (The Build Tool/Bundler):**
    
    - **Development Speed:** Uses Native ESM to serve code instantly without a full bundle step.
    
    - **Production Power:** Uses **Rolldown** (Rust-based) to create highly optimized, small bundles for the end-user.
        
    - **HMR (Hot Module Replacement):** Swaps out code in the browser while maintaining the app's current state.
    
- **The Synergy:** Vite provides the environment (HMR, TypeScript support, Asset loading) that makes writing React code feel instantaneous.
    

### **Cues**

- **Why** use React? (Declarative, reusable components, massive ecosystem)
- **How** does Vite speed up React? (Native ESM + Rust-based Rolldown)    
- **What** is "The Compiler"? (React 19's tool to automate performance)    
- **When** does Vite use Rolldown? (Primarily for production builds and dependency optimization)    

### **Summary**

React is a library for building user interfaces through reusable components and declarative state management. Vite is the development infrastructure that makes building React apps viable at scale by providing near-instant feedback loops. In 2026, the combination of the **React Compiler** and **Vite’s Rolldown engine** has virtually eliminated manual performance tuning and long build times.

### **Related notes**
[[Declarative UI]]
[[React Component Model]]
[[React 19 compiler]]
[[Native ESM Serving (Vite)]]
[[Rolldown Engine]]
[[Vite Hot Module Replacement (HMR)]]
[[JSX (JavaScript XML)]]
[[React-Vite Plugin Integration]]
