# Project Idea
- [/] Movie Search
	- frontend - react
# Introduction to react
- React is a hybrid of javascript and html and uses jsx file extension
- React uses components to build good looking interface
- A component is a modular reusable block of code for an element in the webpage
- Ex: button, headings, dashboards etc,
- Using pre-defined components makes the development easy and fast
- React can be installed with node.js
- Create vite@latest at project location
	- `npm create vite@latest`
- Components start with a capital letter
- A component can only return one component / parent
- To return more than one parent we use fragment `<></>`
- React uses `className` instead of `class`
# Conditional Rendering
- Render components based on a condition
 **Method 1**
```react
{movieNumber === 1 ? (
	<MovieCard movie={{ title: "Avatar", release_date: "2024" }} />
) : (
	<MovieCard movie={{ title: "Bahubali", release_date: "2020" }} />
)}
```
**Method 2**
```react
{movieNumber === 1 && <MovieCard movie={{ title: "Avatar", release_date: "2024" }} />}
```
# Map function
- `map()` maps the elements to components 
```react
movies.map((movie) => (<MovieCard movie={movie} key={movie.id} />))
```
# State
- A state in react is data of a component that can change over time
- When variables use state, any changes to the variable re-renders the component automatically
```react
const [searchQuery, setSearchQuery] = useState("");
```
- When a state changes the entire component will be re renders
- When you want a variable to persist, then it needs to use state
# Page routing in react
- Install `react-router-dom` with `npm install react-router-dom`
- Import `BrowserRouter` to main.jsx with `import { BrowserRouter } from "react-router-dom"`
- When render the app.jsx through BrowserRouter in main.jsx
```react
<BrowserRouter>
	<App />
</BrowserRouter>
```