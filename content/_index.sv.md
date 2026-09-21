---
title: "Välkommen till Papelon"
# Open Graph share-card image. The homepage layout renders covers inside the
# posts loop only, never for the page itself, so this changes the link
# preview and nothing visible on the page.
cover: "images/social-card.png"
---

<!-- ===================================================================
     SWEDISH - DRAFT TRANSLATION, NEEDS A NATIVE SPEAKER

     This is a careful draft, not a native one. It should be grammatical and
     readable, but the voice will not be as warm and offhand as the English.
     Joel should go over it, in particular:
       - "gang" for "a bunch of" - is that the right register?
       - "hobbyn" vs "hobbyn var" and similar definite forms
       - anything that reads as translated rather than written

     English original for reference: content/_index.md
     =================================================================== -->



<!--<form class="retro-single-form" action="https://api.web3forms.com/submit" method="POST">-->

  <!-- Your secret Web3Forms Access Key (Keeps your email hidden!) -->
  <!--<input type="hidden" name="access_key" value="YOUR_ACCESS_KEY_HERE">-->

<!-- The 'onsubmit' part freezes the form so it never leaves the page -->
<form class="retro-single-form" id="kickstarter-form" action="https://api.web3forms.com/submit" method="POST" style="flex: 0 0 60%; max-width: 60%; margin-top: -25px; margin-left: auto; margin-right: auto;">
  <!-- 1. YOUR WEB3FORMS ACCESS KEY (Paste your key here) -->
  <input type="hidden" name="access_key" value="110d46e0-a47e-42bf-b904-a856eca735e7">

  <!-- 2. OPTIONAL: Custom subject line for emails you receive -->
  <input type="hidden" name="subject" value="New Kickstarter Subscriber!">

  <!-- 3. OPTIONAL: Spam protection honeypot -->
  <input type="checkbox" name="botcheck" class="hidden" style="display: none;">
  <!-- Header Text -->
  <p class="retro-form-title">Följ vårt projekt!</p>
  
  <!-- Email Input Box -->
  <input type="email" name="email" placeholder="Skriv din e-post..." required autocomplete="off">

  <!-- Submit Button -->
  <button type="submit" class="submit-btn" id="submit-btn">Följ</button>

  <!-- Message placeholder (shows thank you or error message here) -->
  <p id="form-result" role="status" aria-live="polite" style="margin-top: 10px; font-weight: bold; min-height: 1.5em;">&nbsp;</p>

  <img src="/images/Kickstarter-logo.png" alt="Kickstarter" style="
        max-width: 65%; 
        height: auto; 
        max-height: 360px; 
        object-fit: contain; 
        image-rendering: smooth !important;
        display: block;
        margin: 12px auto 0 !important;
      "/>

</form>

<script>
  const form = document.getElementById("kickstarter-form");
  const result = document.getElementById("form-result");
  const button = document.getElementById("submit-btn");

  // How long to wait before giving up. Without this the request can hang
  // indefinitely, leaving the button disabled and the user staring at
  // "Skickar..." with no way to retry.
  const TIMEOUT_MS = 10000;

  form.addEventListener("submit", function (e) {
    e.preventDefault();

    button.disabled = true;
    result.style.color = "";
    result.innerText = "Skickar...";

    const controller = new AbortController();
    const timer = setTimeout(() => controller.abort(), TIMEOUT_MS);

    const json = JSON.stringify(Object.fromEntries(new FormData(form)));

    fetch("https://api.web3forms.com/submit", {
      method: "POST",
      headers: { "Content-Type": "application/json", Accept: "application/json" },
      body: json,
      signal: controller.signal
    })
      .then(async (response) => {
        const res = await response.json().catch(() => ({}));
        if (response.ok) {
          result.style.color = "green";
          result.innerText = "Tack för att du prenumererar! 🎉";
          form.reset();
        } else {
          result.style.color = "red";
          result.innerText = res.message || "Något gick fel. Försök igen.";
        }
      })
      .catch((error) => {
        result.style.color = "red";
        result.innerText = error.name === "AbortError"
          ? "Det här tar längre tid än väntat. Kontrollera din anslutning och försök igen."
          : "Kunde inte nå servern. Försök igen.";
      })
      .finally(() => {
        clearTimeout(timer);
        button.disabled = false;
      });
  });
</script>

# ⌗ Välkommen till Papelon
>Hej! Vi är ett gäng <kbd class="kbd-yellow">speldesigners</kbd> från olika delar av världen som samlats på en liten kalkstensö mitt i <kbd class="kbd-red">Östersjön</kbd>. Tillsammans driver vi en liten <kbd class="kbd-blue">brädspelsstudio</kbd> med målet att göra hobbyn mer <kbd class="kbd-pink">tillgänglig</kbd>, både för spelare och för designers.
>
>Hjälp oss att sätta vind i seglen på våra <kbd class="kbd-purple">två första spel</kbd> på <kbd>Kickstarter</kbd>! Vill du veta mer om studion eller vad vi håller på att skapa, kolla in här nedanför <kbd class="kbd-green">:D</kbd> 

<!-- Container for side-by-side game boxes -->
<div class="games-container" style="display: flex; align-items: center; justify-content: center;">

  <!-- Left Game Box -->
  <div class="game-box game-yellow game-box--logo" style="flex: 0 0 35%; max-width: 35%;">
    <img src="/images/logos/hamla-logo.png" alt="Hamla" />
  </div>

  <div class="game-separator separator-green" style="margin: 0 15px;">+</div>
  
  <!-- Right Game Box -->
  <div class="game-box game-blue game-box--logo" style="flex: 0 0 35%; max-width: 35%;">
    <img src="/images/logos/essom_3-05.png" alt="Essom" />
  </div>

</div>
