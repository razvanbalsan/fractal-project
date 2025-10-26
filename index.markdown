---
layout: single
title: "Falimentează firma pentru o cauză bună"
header:
  overlay_image: /assets/images/poor_sorin.jpg
  teaser: /assets/images/poor_sorin.jpg
  # overlay_filter: 0.5  # Optional: adds a dark overlay for better text contrast
gallery1:
  - url: /assets/images/poor_sorin.jpg
    image_path: /assets/images/poor_sorin.jpg
  - url: /assets/images/sorin-face-swap.png
    image_path: /assets/images/sorin-face-swap.png
  - url: /assets/images/sorin-face-swap2.png
    image_path: /assets/images/sorin-face-swap2.png
footer:
  content: "© 2024 Boatyardx Team Christmas Charity."
---

{% include gallery id="gallery1" caption="" %}

Se apropie Crăciunul — perioada în care, teoretic, nimeni nu cheltuie bani, nu-i așa? Ei bine, m-am gândit să profit un pic de generozitatea voastră, și nu doar atât. Vrem să strângem niște bănuți pentru a sprijini [Casa de Copii Căsuța Bucuriei](https://www.casutabucuriei.eu/).

Partea cea mai frumoasă este că l-am prins pe Sorin într-o dispoziție excelentă, iar anul acesta Boatyardx o să dubleze fiecare leu pe care îl donăm noi!

Ho ho! Orice contribuție, oricât de mică, ajută enorm.

Cine dorește să ajute, poate trimite donațiile până pe 20 decembrie la:

**Revolut:** @razvanbalsan  
**ING:** RO93INGB0000999905486139  
**Nume:** Razvan Balsan  
**Detalii plată:** BYX Christmas

<div id="fetched-value" style="font-size:1.5em; font-weight:bold; text-align:center; margin-top:20px;"></div>

## Au mai ramas:
{: .text-center}

<div id="countdown" style="font-size:2em; font-weight:bold; text-align:center; margin-top:50px;"></div>


<script>
(function() {
  var countDownDate = new Date("Dec 20, 2024 20:00:00 GMT+0200").getTime();

  // Function to fetch and update the fetched value
function fetchAndUpdateValue() {
  fetch('https://docs.google.com/spreadsheets/d/e/2PACX-1vROjsHIF-GmltYCqh3cwRwqpMIhvXZGOT_aXMEzmCZFmcCwspGeTs7AQfkf21nYp0fDZXJS7GXc__J1/pub?gid=0&single=true&output=csv', {
    cache: "no-cache"
  })
    .then(response => response.text())
    .then(data => {
      const rows = data.split('\n').map(row => row.split(','));
      const fetchedValue = rows[0][0]; 
      
      // Update the fetched value in the DOM with multi-line text
      const fetchedValueDiv = document.getElementById('fetched-value');
      fetchedValueDiv.innerHTML = `
        <div style="text-align: center;">Până acum, Boatyardx e cu</div>
        <div style="text-align: center; font-size: 1.5em; font-weight: bold; color: red;">${fetchedValue} lei</div>
        <div style="text-align: center;">mai săracă</div>
      `;
    })
    .catch(error => console.error('Error:', error));
}


  // Function to update the countdown
  function updateCountdown() {
    var now = new Date().getTime();
    var distance = countDownDate - now;

    if (distance < 0) {
      clearInterval(x);
      document.getElementById("countdown").textContent = "DING DING DING!";
      return;
    }

    var days = Math.floor(distance / (1000 * 60 * 60 * 24));
    var hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
    var minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
    var seconds = Math.floor((distance % (1000 * 60)) / 1000);

    // Update the countdown text
    const countdownDiv = document.getElementById("countdown");
    countdownDiv.textContent = 
      days + " zile " + hours + " ore " + minutes + " min " + seconds + " sec ";

    // Change countdown colour to red if 1 day or less is remaining
    if (days < 1) {
      countdownDiv.style.color = "red";
      countdownDiv.style.fontWeight = "bold";
    } else {
      countdownDiv.style.color = ""; // Reset to default
      countdownDiv.style.fontWeight = "";
    }
  }

  // Fetch value and update countdown initially
  fetchAndUpdateValue();
  updateCountdown();

  // Auto-update the fetched value every 5 seconds
  setInterval(fetchAndUpdateValue, 10000);

  // Update the countdown every second
  var x = setInterval(updateCountdown, 1000);
})();
</script>
