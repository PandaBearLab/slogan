<template>
    <div class="contact-info">
      <h1>Contact Information</h1>
      <ul>
        <!-- <li>
          <i class="fas fa-envelope"></i>
          <a :href="`mailto:${email}`">{{ email }}</a>
        </li>
        <li>
          <i class="fas fa-globe"></i>
          <a :href="website" target="_blank">{{ website }}</a>
        </li> -->
        <li>
          <img src="/avatar.jpg" alt="Twitter Logo" class="twitter-logo" />
          <a :href="twitter" target="_blank">{{ twitter }}</a>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    name: 'ContactInfo',
    data() {
      return {
        email: 'example@example.com',
        website: 'https://example.com',
        twitter: 'https://twitter.com/mrbear1024'
      };
    }
  }
  </script>
  
  <style scoped>
  .contact-info {
    font-family: Arial, sans-serif;
    /* max-width: 400px; */
    margin: 0 auto;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 8px;
    background-color: #f9f9f9;
    
  }
  .contact-info h1 {
    font-size: 24px;
    margin-bottom: 20px;
    text-align: center;
  }
  .contact-info ul {
    list-style: none;
    padding: 0;
    align-items: center;
  }
  .contact-info li {
    display: flex;
    align-items: center;
    justify-content: center; /* 将内容居中对齐 */
    margin-bottom: 10px;
  }

  .contact-info i {
    margin-right: 10px;
    color: #4299e1;
  }
  .contact-info .twitter-logo {
    width: 24px;
    height: 24px;
    margin-right: 10px;
  }
  .contact-info a {
    color: #4299e1;
    text-decoration: none;
  }
  .contact-info a:hover {
    text-decoration: underline;
  }
  </style>