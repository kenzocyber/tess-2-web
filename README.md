# tess-2-web
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Kenzo | Ethical Hacker</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    body {
      margin: 0;
      background: linear-gradient(180deg, #0c0c1d, #05050a, #000);
      color: #e0f7fa;
      font-family: 'JetBrains Mono', monospace;
    }

    .container {
      max-width: 420px;
      margin: auto;
      padding: 1rem;
      position: relative;
      z-index: 10;
    }

    /* Card */
    .card {
      border: 1px solid #00fff7;
      border-radius: 0.5rem;
      padding: 1rem;
      background: rgba(17, 25, 40, 0.85);
      transition: all 0.3s ease-in-out;
    }
    .card:hover {
      transform: scale(1.03);
      box-shadow: 0 0 15px #00fff7;
    }

    /* Fade effect */
    .fade {
      opacity: 0;
      transform: scale(0.95);
      transition: all 0.3s ease-in-out;
    }
    .fade.show {
      opacity: 1;
      transform: scale(1);
    }

    /* Matrix Rain */
    canvas#matrix {
      position: fixed;
      top: 0;
      left: 0;
      z-index: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
      opacity: 0.25;
    }

    /* Search input */
    .search-box {
      border: 1px solid #00fff7;
      border-radius: 0.5rem;
      padding: 0.5rem;
      background: rgba(0,0,0,0.6);
      width: 100%;
      margin-bottom: 1rem;
      outline: none;
      color: #00fff7;
    }
  </style>
</head>
<body>
  <canvas id="matrix"></canvas>

  <div class="container">
    <header class="text-center mb-4">
      <h1 class="text-xl font-bold text-cyan-400">Kenzo — Ethical Hacker</h1>
      <p class="text-sm text-cyan-300">Security Researcher & Pentester</p>
    </header>

    <!-- 🔍 Search Box -->
    <input type="text" id="search" class="search-box" placeholder="🔍 Cari skills, project, atau kontak...">

    <section class="card mb-4 searchable" data-keywords="about me kenzo hacker ethical security pentest">
      <h2 class="text-base mb-2">About Me</h2>
      <p class="text-sm">Saya Kenzo, fokus dalam ethical hacking & keamanan siber. Misi saya adalah mengamankan sistem, memburu celah, & berbagi ilmu.</p>
    </section>

    <section class="mb-4">
      <h2 class="text-base mb-2">Skills</h2>
      <div class="space-y-2">
        <div class="card searchable" data-keywords="web app pentesting skill">Web App Pentesting ⭐⭐⭐⭐⭐</div>
        <div class="card searchable" data-keywords="api security skill">API Security ⭐⭐⭐⭐☆</div>
        <div class="card searchable" data-keywords="network hardening skill">Network Hardening ⭐⭐⭐⭐☆</div>
        <div class="card searchable" data-keywords="reverse engineering skill">Reverse Engineering ⭐⭐⭐☆☆</div>
        <div class="card searchable" data-keywords="osint threat intel skill">OSINT & Threat Intel ⭐⭐⭐⭐⭐</div>
      </div>
    </section>

    <section class="mb-4">
      <h2 class="text-base mb-2">Projects</h2>
      <div class="space-y-2">
        <div class="card searchable" data-keywords="enterprise audit project">Enterprise Audit ⭐⭐⭐⭐⭐</div>
        <div class="card searchable" data-keywords="cloud infra review project">Cloud Infra Review ⭐⭐⭐⭐☆</div>
        <div class="card searchable" data-keywords="bug bounty findings project">Bug Bounty Findings ⭐⭐⭐⭐⭐</div>
        <div class="card searchable" data-keywords="api security hardening project">API Security Hardening ⭐⭐⭐⭐☆</div>
      </div>
    </section>

    <footer class="mt-6 text-center text-[12px] text-cyan-400">
      <p class="searchable" data-keywords="gmail email kontak pykcyber@gmail.com">📧 <a href="mailto:pykcyber@gmail.com" class="underline">pykcyber@gmail.com</a></p>
      <p class="searchable" data-keywords="whatsapp wa kontak 6283143490913">📱 <a href="https://wa.me/6283143490913" target="_blank" class="underline">+62 831-4349-0913</a></p>
      <p class="text-[10px] mt-4">© 2025 Kenzo — Semua hak cipta dilindungi.</p>
    </footer>
  </div>

  <script>
    // MATRIX RAIN
    const canvas = document.getElementById("matrix");
    const ctx = canvas.getContext("2d");

    canvas.height = window.innerHeight;
    canvas.width = window.innerWidth;

    const chars = "01";
    const fontSize = 14;
    const columns = canvas.width / fontSize;
    const drops = [];

    for (let x = 0; x < columns; x++) drops[x] = 1;

    function draw() {
      ctx.fillStyle = "rgba(0, 0, 0, 0.05)";
      ctx.fillRect(0, 0, canvas.width, canvas.height);

      ctx.fillStyle = "#00ff00";
      ctx.font = fontSize + "px monospace";

      for (let i = 0; i < drops.length; i++) {
        const text = chars.charAt(Math.floor(Math.random() * chars.length));
        ctx.fillText(text, i * fontSize, drops[i] * fontSize);

        if (drops[i] * fontSize > canvas.height && Math.random() > 0.975) {
          drops[i] = 0;
        }
        drops[i]++;
      }
    }

    setInterval(draw, 40);

    // 🔍 SEARCH FEATURE
    const searchInput = document.getElementById("search");
    const items = document.querySelectorAll(".searchable");

    searchInput.addEventListener("input", function () {
      const query = this.value.toLowerCase();

      items.forEach(item => {
        const keywords = item.getAttribute("data-keywords").toLowerCase();
        if (keywords.includes(query)) {
          item.classList.add("fade", "show");
          item.style.display = "block";
          setTimeout(() => item.classList.add("show"), 10);
        } else {
          item.classList.remove("show");
          setTimeout(() => item.style.display = "none", 300);
        }
      });
    });
  </script>
</body>
</html>
