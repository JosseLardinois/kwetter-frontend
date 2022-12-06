<template>
    <div class="sidebar">
      <div class="sidebar__header">
        <div class="sidebar__header__title">
          <h1>Sharify</h1>
        </div>
      </div>
      <div class="sidebar__menu">
        <ul>
          <router-link to="/">
            <li>
              <font-awesome-icon icon="fa-solid fa-chart-pie" />
              <span>Overview</span>
            </li>
          </router-link>
          <router-link to="/">
            <li>
              <font-awesome-icon icon="fa-solid fa-magnifying-glass" />
              <span>Home</span>
            </li>
          </router-link>
          <router-link to="/about">
            <li>
              <font-awesome-icon icon="fa-solid fa-people-roof" />
              <span>About</span>
            </li>
          </router-link>
        </ul>
        <ul>
          <router-link to="/">
            <li>
              <font-awesome-icon icon="fa-solid fa-gear" />
              <span>Settings</span>
            </li>
          </router-link>
          <router-link to="/">
            <li>
              <font-awesome-icon icon="fa-solid fa-users" />
              <span>Profile</span>
            </li>
          </router-link>
        </ul>
      </div>
    </div>
  </template>
  
  <style scoped>
  .sidebar {
    height: 100vh;
    background-color: #363740;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    position: fixed;
    left: 0;
    top: 0;
    z-index: 1;
  }
  
  .sidebar__header {
    height: 100px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 20px;
  }
  
  .sidebar__header__title {
    display: flex;
    align-items: center;
    color: #a4a6b3;
  }
  
  .sidebar__header__title img {
    width: 40px;
    height: 40px;
    margin-right: 5px;
  }
  
  .sidebar__menu ul {
    list-style: none;
    padding: 0;
    margin: 0;
  }
  
  .sidebar__menu ul:first-child {
    border-bottom: 1px solid #eee;
  }
  
  .sidebar__menu ul li {
    display: flex;
    align-items: center;
    text-decoration: none;
    color: #a4a6b3;
    padding: 10px 20px;
    height: 2rem;
    color: #a4a6b3;
  }
  
  .sidebar__menu a {
    text-decoration: none;
    color: #a4a6b3;
  }
  
  .sidebar__menu ul li svg {
    margin-right: 15px;
    width: 20px;
  }
  
  .sidebar__menu ul li:hover {
    background-color: #eee;
  }
  </style>
  