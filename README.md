# Task4
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Full Project Page</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0; padding: 0;
      background: #f5f5f5;
    }

    header, section {
      padding: 20px;
      max-width: 1000px;
      margin: auto;
    }

    nav {
      background: #333;
      padding: 10px;
      text-align: center;
    }

    nav a {
      color: white;
      margin: 0 15px;
      text-decoration: none;
    }

    h2 {
      color: #333;
      border-bottom: 2px solid #ccc;
    }

    .project, .product {
      background: white;
      margin: 10px 0;
      padding: 15px;
      border-radius: 5px;
      box-shadow: 0 0 10px #ccc;
    }

    /* To-do styles */
    #todo-section input, #todo-section button {
      padding: 10px;
      margin: 5px;
    }

    .todo-item {
      display: flex;
      justify-content: space-between;
      margin-top: 5px;
    }

    /* Product filter styles */
    .filters {
      margin-bottom: 10px;
    }

    .filters select {
      margin-right: 10px;
    }

    @media (max-width: 768px) {
      nav a {
        display: block;
        margin: 10px 0;
      }
    }
  </style>
</head>
<body>

<nav>
  <a href="#about">About</a>
  <a href="#projects">Projects</a>
  <a href="#contact">Contact</a>
  <a href="#todo-section">To-Do</a>
  <a href="#product-section">Products</a>
</nav>

<section id="about">
  <h2>About Me</h2>
  <p>Hello! I'm a passionate web developer with experience in HTML, CSS, and JavaScript. I build responsive and interactive websites and apps.</p>
</section>

<section id="projects">
  <h2>Projects</h2>
  <div class="project"><strong>Portfolio Website</strong> - Built with HTML, CSS, and JS.</div>
  <div class="project"><strong>To-Do App</strong> - Includes local storage and real-time task updates.</div>
  <div class="project"><strong>Product Filter</strong> - Dynamic filtering and sorting using JavaScript.</div>
</section>

<section id="contact">
  <h2>Contact Me</h2>
  <form>
    <input type="text" placeholder="Your Name" required><br>
    <input type="email" placeholder="Your Email" required><br>
    <textarea placeholder="Your Message" rows="5" required></textarea><br>
    <button type="submit">Send</button>
  </form>
</section>

<section id="todo-section">
  <h2>To-Do List</h2>
  <input type="text" id="todo-input" placeholder="Add a new task">
  <button onclick="addTask()">Add Task</button>
  <div id="todo-list"></div>
</section>

<section id="product-section">
  <h2>Product Listing</h2>
  <div class="filters">
    <select id="category-filter" onchange="filterProducts()">
      <option value="all">All Categories</option>
      <option value="electronics">Electronics</option>
      <option value="clothing">Clothing</option>
    </select>
    <select id="sort-by" onchange="sortProducts()">
      <option value="default">Sort By</option>
      <option value="price">Price</option>
      <option value="rating">Rating</option>
    </select>
  </div>
  <div id="product-list"></div>
</section>

<script>
  // TO-DO APP
  let tasks = JSON.parse(localStorage.getItem("tasks")) || [];

  function renderTasks() {
    const list = document.getElementById("todo-list");
    list.innerHTML = '';
    tasks.forEach((task, i) => {
      list.innerHTML += `
        <div class="todo-item">
          <span>${task}</span>
          <button onclick="deleteTask(${i})">X</button>
        </div>
      `;
    });
  }

  function addTask() {
    const input = document.getElementById("todo-input");
    if (input.value.trim() !== "") {
      tasks.push(input.value.trim());
      localStorage.setItem("tasks", JSON.stringify(tasks));
      input.value = '';
      renderTasks();
    }
  }

  function deleteTask(index) {
    tasks.splice(index, 1);
    localStorage.setItem("tasks", JSON.stringify(tasks));
    renderTasks();
  }

  renderTasks();

  // PRODUCT LISTING
  const products = [
    { name: "Smartphone", category: "electronics", price: 299, rating: 4.5 },
    { name: "Jeans", category: "clothing", price: 49, rating: 4.0 },
    { name: "Laptop", category: "electronics", price: 999, rating: 4.8 },
    { name: "T-Shirt", category: "clothing", price: 19, rating: 3.9 }
  ];

  function displayProducts(list) {
    const container = document.getElementById("product-list");
    container.innerHTML = '';
    list.forEach(p => {
      container.innerHTML += `
        <div class="product">
          <strong>${p.name}</strong><br>
          Category: ${p.category} <br>
          Price: $${p.price} <br>
          Rating: ${p.rating}
        </div>
      `;
    });
  }

  function filterProducts() {
    const category = document.getElementById("category-filter").value;
    let filtered = products;
    if (category !== "all") {
      filtered = products.filter(p => p.category === category);
    }
    displayProducts(filtered);
  }

  function sortProducts() {
    const sortBy = document.getElementById("sort-by").value;
    let sorted = [...products];
    if (sortBy === "price") {
      sorted.sort((a, b) => a.price - b.price);
    } else if (sortBy === "rating") {
      sorted.sort((a, b) => b.rating - a.rating);
    }
    displayProducts(sorted);
  }

  displayProducts(products);
</script>

</body>
</html>
