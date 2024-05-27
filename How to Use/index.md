---
icon: "book"
---

Welcome to the DotnetBaseKit How to Use section! This documentation provides an overview of how to use the various parts of the components included in DotnetBaseKit. You`ll learn how to use our Responses, Notiifications, Paginations, Validations and many more.

## Getting Started

To get started, simply select a part from the list below (or in the menu on the left) to learn more about its features and examples. 

Explore each component to discover how DotnetBaseKit can help you build better .NET applications. Let's dive in!

<head>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
</head>

<style>
.card-container {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 15px;
  justify-content: center;
}

.card-container a {
  text-decoration: none;
}

.card {
  display: flex;
  flex-direction: column;
  align-items: center;
  background: rgba(20, 23, 26, 0.25);
  background: rgba(20, 23, 26, 0.25) linear-gradient(to right bottom, rgba(0, 59, 117, 0.1) 25%, rgba(20, 23, 26, 0.2) 100%);
  border: 1px solid rgb(29, 33, 38);
  border-radius: 8px;
  color: inherit;
  transition: transform 0.2s, border-color 0.2s;
  color: white;
  box-sizing: border-box;
  cursor: pointer;
  text-decoration: none !important;
  padding: 16px;
}

.card:hover {
  transform: scale(1.05);
  border-color: rgba(0, 107, 214, 0.5);
}

.card-content {
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: center;
  height: 100%;
}

.card h3 {
  margin-top: 10px;
}

.card p {
  margin: 0;
  color: #adadad;
  font-size: 14px;
  line-height: 1.4;
  text-align: start;
}

.icon-wrapper {
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 8px;
  font-size: 24px;
  border: 1px solid rgba(51, 153, 255, 0.25);
  border-radius: 5px;
  background-color: #08233f;
}

.icon-wrapper i {
  color: #3399ff;
}

@media (max-width: 1024px) {
  .card-container {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 768px) {
  .card-container {
    grid-template-columns: repeat(1, 1fr);
  }

  .card p {
    font-size: 12px;
  }
}

@media (max-width: 480px) {
  .card p {
    font-size: 10px;
  }
}
</style>

<div class="card-container">
  <a href="responses" class="card">
    <div class="card-content">
      <h3>Responses</h3>
      <p>Common functionality for WebApi to simplify response creation with custom responses.</p>
    </div>
  </a>

  <a href="pagination" class="card">
    <div class="card-content">
      <h3>Pagination</h3>
      <p>Efficiently manage large data sets by breaking them into manageable chunks.</p>
    </div>
  </a>

  <a href="validations" class="card">
    <div class="card-content">
      <h3>Validations</h3>
      <p>Ensure that data received and processed by the application is correct and well-formed.</p>
    </div>
  </a>
  
  <a href="database-mapping" class="card">
     <div class="card-content">
      <h3>Database Mapping / Config</h3>
      <p>Configure database mapping using Fluent API in .NET.</p>
    </div>
  </a>

  <a href="migrations" class="card">
     <div class="card-content">
      <h3>Migrations</h3>
      <p>Keep your database schema in sync with your data model over time.</p>
    </div>
  </a>

  <a href="full-project" class="card">
    <div class="card-content">
      <h3>Full Project</h3>
      <p>Comprehensive view of the entire project, showcasing how components interconnect.</p>
    </div>
  </a> 
</div>
