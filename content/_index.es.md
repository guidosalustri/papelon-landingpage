---
title: "Bienvenidos a Papelon"
# Open Graph share-card image. The homepage layout renders covers inside the
# posts loop only, never for the page itself, so this changes the link
# preview and nothing visible on the page.
cover: "images/social-card.png"
---

<!-- ===================================================================
     SPANISH - DRAFT TRANSLATION, PLEASE REVIEW

     Written in neutral Latin American Spanish (tuteo: "quieres", "mira").
     If you would rather it sounded Argentine (voseo: "querés", "mirá"),
     say so and it can be switched throughout - it is a consistent change,
     not a rewrite.

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
  <p class="retro-form-title">¡Sigue nuestro proyecto!</p>
  
  <!-- Email Input Box -->
  <input type="email" name="email" placeholder="Escribe tu correo..." required autocomplete="off">

  <!-- Submit Button -->
  <button type="submit" class="submit-btn" id="submit-btn">Seguir</button>

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
  // "Enviando..." with no way to retry.
  const TIMEOUT_MS = 10000;

  form.addEventListener("submit", function (e) {
    e.preventDefault();

    button.disabled = true;
    result.style.color = "";
    result.innerText = "Enviando...";

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
          result.innerText = "¡Gracias por suscribirte! 🎉";
          form.reset();
        } else {
          result.style.color = "red";
          result.innerText = res.message || "Algo salió mal. Intenta de nuevo.";
        }
      })
      .catch((error) => {
        result.style.color = "red";
        result.innerText = error.name === "AbortError"
          ? "Está tardando más de lo esperado. Revisa tu conexión e intenta de nuevo."
          : "No se pudo conectar con el servidor. Intenta de nuevo.";
      })
      .finally(() => {
        clearTimeout(timer);
        button.disabled = false;
      });
  });
</script>

# ⌗ Bienvenidos a Papelon
>¡Hola! Somos un grupo de <kbd class="kbd-yellow">diseñadores de juegos</kbd> de distintas partes del mundo, que terminamos en una isla de piedra caliza en medio del <kbd class="kbd-red">mar Báltico</kbd>. Juntos llevamos un pequeño <kbd class="kbd-blue">estudio de juegos de mesa</kbd> que busca hacer el hobby más <kbd class="kbd-pink">accesible</kbd>, tanto para diseñadores como para jugadores.
>
>¡Ayúdanos a dar vida a nuestros <kbd class="kbd-purple">dos primeros juegos</kbd> en <kbd>Kickstarter</kbd>! Y si te interesa saber más sobre el estudio o sobre lo que estamos creando, abajo puedes encontrar más info <kbd class="kbd-green">:D</kbd> 

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
