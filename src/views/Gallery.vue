<template>
    <div class="not-found">
      <div class="content">
        <div class="icon">
          <svg xmlns="http://www.w3.org/2000/svg" width="120" height="120" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <circle cx="12" cy="12" r="10" />
            <path d="M15 9l-6 6M9 9l6 6" />
          </svg>
        </div>
        <h1>404</h1>
        <p>Страница в разработке</p>
        <router-link to="/" class="back-button">Вернуться на главную</router-link>
      </div>
    </div>
  </template>
  
  <script>
  export default {};
  </script>
  
  <style scoped>
  .not-found {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-color: #e8d9cf;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    margin: 0;
    overflow: hidden;
  }
  
  .content {
    text-align: center;
    padding: 40px 60px;
    border-radius: 12px;
    box-shadow: 0 8px 20px rgba(103, 69, 69, 0.1);
    transform: scale(0.8);
    animation: scaleIn 0.6s ease-out forwards;
  }
  
  .icon {
    margin-bottom: 20px;
    animation: rotate 4s infinite linear;
  }
  
  .icon svg {
    fill: #e8d9cf;
    width: 120px;
    height: 120px;
  }
  
  h1 {
    font-size: 6rem;
    font-weight: 700;
    color: #757575;
    margin: 20px 0;
    opacity: 0;
    animation: fadeIn 1s ease-out 0.5s forwards;
  }
  
  p {
    font-size: 1.5rem;
    color: #757575;
    margin-bottom: 30px;
    opacity: 0;
    animation: fadeIn 1s ease-out 1s forwards;
  }
  
  .back-button {
    padding: 14px 28px;
    font-size: 1.2rem;
    background-color: #a1958c;
    color: white;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    text-decoration: none;
    display: inline-block;
    transform: translateY(10px);
    opacity: 0;
    animation: fadeIn 1s ease-out 1.5s forwards, moveUp 0.6s ease-out 1.5s forwards;
  }
  
  .back-button:hover {
    background-color: #0c0b0b;
  }
  
  @keyframes rotate {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }
  
  @keyframes fadeIn {
    0% {
      opacity: 0;
    }
    100% {
      opacity: 1;
    }
  }
  
  @keyframes moveUp {
    0% {
      transform: translateY(10px);
    }
    100% {
      transform: translateY(0);
    }
  }
  
  @keyframes scaleIn {
    0% {
      transform: scale(0.8);
      opacity: 0;
    }
    100% {
      transform: scale(1);
      opacity: 1;
    }
  }
  </style>
  