---
icon: "tools"
---

Welcome to the DotnetBaseKit Components section! This documentation provides an overview of the various components included in DotnetBaseKit, each designed to streamline and enhance specific aspects of .NET application development.

## Overview

DotnetBaseKit offer a comprehensive set of tools and functionalities to cover different layers of application architecture, including API development, application logic, domain modeling, and infrastructure management. Whether you're a beginner or an experienced developer, these components aim to simplify the development process and improve overall code quality.

## Getting Started

To get started, simply select a component from the list below (or in the menu on the left) to learn more about its features, installation instructions and examples. Whether you're building a simple web API or a complex application, DotnetBaseKit Components provide the essential building blocks to help you succeed.

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
  <a href="api" class="card">
    <div class="card-content">
      <h3>Api</h3>
      <p>Common functionality for WebApi to simplify response creation with custom response.</p>
    </div>
  </a>

  <a href="application" class="card">
    <div class="card-content">
      <h3>Application</h3>
      <p>Structure of service applications for handling notifications, pagination and more.</p>
    </div>
  </a>
  
  <a href="domain-sql" class="card">
    <div class="card-content">
      <h3>Domain.Sql</h3>
      <p>Offers a structured approach for managing DTOs, entities, and repositories for SQL Databases.</p>
    </div>
  </a>

  <a href="domain-mongodb" class="card">
    <div class="card-content">
      <h3>Domain.MongoDB</h3>
      <p>Offers a structured approach for managing DTOs, entities, and repositories for MongoDB.</p>
    </div>
  </a>

  <a href="infra-sql" class="card">
    <div class="card-content">
      <h3>Infra.Sql</h3>
      <p>Provides the database context and implementations of domain repositories, supporting SQL Server, MySQL, and PostgreSQL.</p>
    </div>
  </a>

  <a href="infra-mongodb" class="card">
    <div class="card-content">
      <h3>Infra.MongoDb</h3>
      <p>Manages MongoDB connections and configurations alongside domain repositories, offering efficient data handling.</p>
    </div>
  </a>

  <a href="shared" class="card">
    <div class="card-content">
      <h3>Shared</h3>
      <p>Contains utility classes for managing notifications, facilitating communication and feedback within the application.</p>
    </div>
  </a>   
