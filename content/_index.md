---
title: "Welcome to Papelon"
---
# Welcome to the Papelon
>Hello there! We are a bunch of <kbd class="kbd-yellow">game designers</kbd> from around the world sitting on top of a small limestone island in the middle of the <kbd class="kbd-red">Baltic Sea</kbd>. Together, we run a tiny <kbd class="kbd-blue">board game studio</kbd> that hopes to make the hobby more <kbd class="kbd-pink">accessible</kbd> for both players and designers.
>
>Join us for the launch of our first <kbd>Kickstarter</kbd> campaign! We are featuring two of <kbd class="kbd-purple">our games!</kbd> If you want to learn more about our studio or the games, you'll find more info below <kbd class="kbd-green">:D</kbd>


<!--<form class="retro-single-form" action="https://api.web3forms.com/submit" method="POST">-->

  <!-- Your secret Web3Forms Access Key (Keeps your email hidden!) -->
  <!--<input type="hidden" name="access_key" value="YOUR_ACCESS_KEY_HERE">-->

<!-- The 'onsubmit' part freezes the form so it never leaves the page -->
<form class="retro-single-form" id="kickstarter-form">
  <!-- 1. YOUR WEB3FORMS ACCESS KEY (Paste your key here) -->
  <input type="hidden" name="access_key" value="110d46e0-a47e-42bf-b904-a856eca735e7">

  <!-- 2. OPTIONAL: Custom subject line for emails you receive -->
  <input type="hidden" name="subject" value="New Kickstarter Subscriber!">

  <!-- 3. OPTIONAL: Spam protection honeypot -->
  <input type="checkbox" name="botcheck" class="hidden" style="display: none;">
  <!-- Header Text -->
  <p class="retro-form-title">Get Kickstarter Updates!</p>
  
  <!-- Email Input Box -->
  <input type="email" name="email" placeholder="Type your email..." required autocomplete="off">

  <!-- Submit Button -->
  <button type="submit" class="submit-btn" id="submit-btn">Follow</button>

  <!-- Message placeholder (shows thank you or error message here) -->
  <p id="form-result" style="margin-top: 10px; font-weight: bold; min-height: 1.5em;">&nbsp;</p>

</form>

<script>
  const form = document.getElementById('kickstarter-form');
  const result = document.getElementById('form-result');
  const button = document.getElementById('submit-btn');

  form.addEventListener('submit', function(e) {
    e.preventDefault();
    
    // Feedback while sending
    button.disabled = true;
    result.innerText = "Submitting...";

    const formData = new FormData(form);
    const json = JSON.stringify(Object.fromEntries(formData));

    fetch('https://api.web3forms.com/submit', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'Accept': 'application/json'
      },
      body: json
    })
    .then(async (response) => {
      let res = await response.json();
      if (response.status === 200) {
        result.style.color = "green";
        result.innerText = "Thanks for subscribing! 🎉";
        form.reset();
      } else {
        result.style.color = "red";
        result.innerText = res.message || "Something went wrong.";
      }
    })
    .catch(error => {
      result.style.color = "red";
      result.innerText = "Error sending message!";
    })
    .finally(() => {
      button.disabled = false;
    });
  });
</script>

<!-- Container for side-by-side game boxes -->
<div class="games-container">

  <!-- Left Game Box -->
  <div class="game-box game-yellow" style="flex: 0 0 35%; max-width: 35%;">
        <img src="/images/hamla-logo.png" style="
        max-width: 80%; 
        height: auto; 
        max-height: 360px; 
        object-fit: contain; 
        image-rendering: smooth !important;
      "/>
  </div>

  <div class="game-separator separator-green">+</div>
  
  <!-- Right Game Box -->
  <div class="game-box game-blue" style="flex: 0 0 35%; max-width: 35%;">
        <img src="/images/essom-logo.png" style="
        max-width: 80%; 
        height: auto; 
        max-height: 360px; 
        object-fit: contain; 
        image-rendering: smooth !important;
      "/>
  </div>
</div>

<img src="/images/kickstarter-logo.png" style="
        max-width: 40%; 
        height: auto; 
        max-height: 360px; 
        object-fit: contain; 
        image-rendering: smooth !important;
        display: block;
        margin: -45px auto !important;
      "/>