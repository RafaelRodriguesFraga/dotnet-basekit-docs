---
icon: "gear"
---

Welcome to the DotnetBaseKit Configuration section! This documentation provides an overview of how to set up and configure your application to use different databases. red to your specific requirements.

## Overview

DotnetBaseKit supports various database systems and offers flexible configuration options to cater to different needs. This section covers configuration for PostgreSQL, MySQL, SQL Server, and MongoDB, providing detailed instructions on how to set up each database

## Getting Started

To get started, select a configuration topic from the list below (or in the menu on the left) to learn more about its settings, usage, and examples. Whether you're setting up a relational database or a NoSQL database like MongoDB, this section will guide you through the necessary steps.

Explore each topic to ensure your DotnetBaseKit application is configured correctly and optimized for your chosen database and logging requirements. Let's dive in!

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
  <a href="sql-dabatase-config" class="card">
    <div class="card-content">
      <h3>SQL Database Config</h3>
      <p>Set up and configure PostgreSQL, MySQL, and SQL Server for your application.</p>
    </div>
  </a>

  <a href="mongodb-database-config" class="card">
    <div class="card-content">
      <h3>MongoDB Database Config</h3>
      <p>Configure MongoDB settings for a seamless integration with your application.</p>
    </div>
  </a>  

  <a href="full-appsettings-config" class="card">
    <div class="card-content">
      <h3>Full Appsettings Config</h3>
      <p>Explore all available options for configuring your appsettings.json file.</p>
    </div>
  </a>  
  </div>

