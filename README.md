<html lang="uz">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Fermerlik darslari — Videolar</title>
  <meta name="description" content="Fermerlik darslari: chorva, dehqonchilik, sabzavotchilik va meva yetishtirish bo'yicha amaliy videolar to'plami." />
  <style>
    :root{
      --accent:#2f6b2f;
      --muted:#333;
      --card:#ffffffcc;
      --glass: rgba(255,255,255,0.08);
      --radius:10px;
      --gap:14px;
    }
    @media (prefers-color-scheme:dark){
      :root{
        --accent:#6bb46b;
        --muted:#ddd;
        --card:#0f1114cc;
        --glass: rgba(0,0,0,0.25);
      }
    }

    *{box-sizing:border-box}
    html,body{height:100%;margin:0;font-family:Inter, Roboto, Arial, sans-serif;color:var(--muted)}
    /* Background image (beautiful farm image). Change URL to use your own. */
    body{
      background-image: url('https://th.bing.com/th/id/OIP.j7wtyBkgvqBa7XPiCzLalQHaDC?w=1200&h=600&c=7&r=0&o=5&pid=1.7');
      background-size: cover;
      background-position: center;
      background-attachment: fixed;
      position: relative;
    }
    /* subtle overlay for readability */
    body::before{
      content:"";
      position:fixed;
      inset:0;
      background: linear-gradient(180deg, rgba(0,0,0,0.35), rgba(255,255,255,0.04));
      pointer-events:none;
      z-index:0;
    }

    .app{display:flex;min-height:100vh;gap:0;position:relative;z-index:1}
    .sidebar{
      width:260px;padding:18px;flex-shrink:0;
      display:flex;flex-direction:column;gap:12px;
      background: linear-gradient(180deg, rgba(47,107,47,0.95), rgba(31,79,31,0.95));
      color:#fff;
      border-right: 1px solid rgba(255,255,255,0.04);
      backdrop-filter: blur(6px);
    }
    .logo{font-weight:700;font-size:1.1rem}
    nav a{color:inherit;text-decoration:none;padding:8px;border-radius:8px;display:block}
    nav a:hover, nav a.active{background:rgba(255,255,255,0.06)}
    .main{flex:1;padding:18px}
    header.header{display:flex;align-items:center;justify-content:space-between;gap:12px;margin-bottom:12px}
    .controls{display:flex;gap:10px;align-items:center}
    .search{padding:8px;border-radius:8px;border:1px solid rgba(0,0,0,0.08);min-width:180px}
    .video-list{display:grid;gap:var(--gap);grid-template-columns:repeat(auto-fit,minmax(260px,1fr))}
    .video{background:var(--card);padding:12px;border-radius:10px;box-shadow:0 2px 8px rgba(0,0,0,0.12)}
    .video h3{margin:0 0 8px 0;font-size:1rem;color:var(--muted)}
    .thumb{position:relative;border-radius:8px;overflow:hidden;background:#000}
    .thumb img{display:block;width:100%;height:auto;object-fit:cover}
    .play-btn{position:absolute;inset:0;display:flex;align-items:center;justify-content:center;background:linear-gradient(180deg, rgba(0,0,0,0.0), rgba(0,0,0,0.28));color:#fff;font-weight:700;font-size:14px;pointer-events:none}
    .meta{display:flex;justify-content:space-between;align-items:center;margin-top:8px}
    .link{font-size:0.9rem;color:var(--accent);text-decoration:none}

    /* Modal / embedded player styles */
    .video-modal{
      position:fixed;
      inset:0;
      display:none;
      align-items:center;
      justify-content:center;
      background: rgba(0,0,0,0.75);
      z-index:120;
      padding:20px;
    }
    .video-modal.open{display:flex}
    .video-modal-content{
      width:min(1100px,95%);
      max-width:1100px;
      aspect-ratio:16/9;
      background:transparent;
      position:relative;
      border-radius:8px;
      overflow:hidden;
      box-shadow:0 10px 40px rgba(0,0,0,0.6);
    }
    .video-frame iframe{width:100%;height:100%;border:0;display:block}
    .modal-close{
      position:absolute;
      top:8px;
      right:8px;
      background: rgba(255,255,255,0.9);
      color:var(--accent);
      border:0;
      padding:6px 10px;
      border-radius:6px;
      font-weight:700;
      cursor:pointer;
      z-index:2;
    }

    /* Floating call widget: top-right */
    .call-widget{
      position:fixed;
      top:18px;
      right:18px;
      z-index:80;
      display:flex;
      flex-direction:column;
      align-items:center;
      gap:6px;
      font-family:inherit;
    }
    .call-button{
      display:flex;
      align-items:center;
      gap:8px;
      background:linear-gradient(180deg,#ffffffaa, #ffffff88);
      color:var(--accent);
      padding:10px 12px;
      border-radius:999px;
      box-shadow: 0 6px 18px rgba(0,0,0,0.18);
      border: none;
      cursor: pointer;
      font-weight:700;
      backdrop-filter: blur(4px);
    }
    .call-button small{display:block;font-size:0.85rem;color:rgba(0,0,0,0.7)}
    .call-label{
      font-size:0.85rem;
      color:#fff;
      background: rgba(0,0,0,0.36);
      padding:4px 8px;
      border-radius:8px;
      cursor:pointer;
      user-select:none;
    }
    /* panel that appears under "Call" label */
    .call-panel{
      margin-top:8px;
      background: linear-gradient(180deg, rgba(255,255,255,0.95), rgba(255,255,255,0.88));
      color:var(--muted);
      border-radius:10px;
      padding:10px;
      box-shadow: 0 6px 20px rgba(0,0,0,0.25);
      display:none;
      min-width:220px;
      text-align:left;
    }
    .call-panel.open{display:block}
    .call-option{display:flex;justify-content:space-between;align-items:center;padding:8px;border-radius:8px;cursor:pointer;background:transparent}
    .call-option:hover{background:rgba(0,0,0,0.04)}
    .call-option a{color:var(--accent);text-decoration:none;font-weight:600}
    .call-meta{font-size:0.85rem;color:rgba(0,0,0,0.6)}

    /* small close button in panel */
    .call-close{background:transparent;border:0;color:var(--muted);cursor:pointer;font-weight:700;padding:6px}

    /* mobile adjustments */
    @media (max-width:800px){
      .sidebar{position:fixed;left:-320px;top:0;height:100%;z-index:40;transition:left .22s}
      .sidebar.open{left:0}
      .call-widget{right:12px;top:12px}
      .call-panel{min-width:180px}
      .video-modal-content{width:95%;aspect-ratio:16/9}
    }

    /* focus */
    a:focus, button:focus, input:focus{outline:3px solid rgba(47,107,47,0.18);outline-offset:3px}

    footer.site-footer{margin-top:18px;color:rgba(255,255,255,0.95);font-size:0.95rem;text-align:center;padding:12px}
  </style>
</head>
<body>
  <!-- Floating call widget placed at top-right -->
  <div class="call-widget" id="callWidget" aria-live="polite">
    <button class="call-button" id="callButton" aria-haspopup="true" aria-expanded="false" title="Qo'ng'iroq">
      <span style="display:inline-flex;align-items:center;gap:8px">
        <!-- simple phone icon using SVG for crispness -->
        <svg width="18" height="18" viewBox="0 0 24 24" fill="none" aria-hidden="true" focusable="false">
          <path d="M6.62 10.79a15.053 15.053 0 006.59 6.59l2.2-2.2a1 1 0 011.01-.24c1.12.37 2.33.57 3.57.57a1 1 0 011 1V20a1 1 0 01-1 1C10.07 21 3 13.93 3 5a1 1 0 011-1h3.5a1 1 0 011 1c0 1.24.2 2.45.57 3.57.12.35 0 .74-.24 1.01l-2.21 2.21z" fill="currentColor"/>
        </svg>
        <span>+998 94 258 60 45</span>
      </span>
      <small style="margin-left:6px">CALL</small>
    </button>

    <!-- a visible label under button which also toggles the panel -->
    <div id="callLabel" class="call-label" role="button" tabindex="0" aria-controls="callPanel" aria-expanded="false">Call</div>

    <!-- hidden panel shown when pressing label -->
    <div id="callPanel" class="call-panel" role="dialog" aria-hidden="true" aria-label="Call options">
      <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:6px">
        <strong>Bog'lanish</strong>
        <button class="call-close" id="callPanelClose" aria-label="Yopish">✕</button>
      </div>
      <div class="call-option" id="makeCall">
        <span>To'g'ridan-to'g'ri qo'ng'iroq</span>
        <a href="tel:+998942586045" id="telLink">Call</a>
      </div>
      <div class="call-option" id="copyNumber" style="margin-top:6px">
        <span>Raqamni nusxalash</span>
        <button id="copyBtn" class="call-close" aria-label="Nusxalash">Copy</button>
      </div>
      <div style="margin-top:8px;font-size:0.9rem;color:rgba(0,0,0,0.6)">
        Qo'ng'iroq ishlamasa, raqamni nusxalab telefoningizdan qo'ng'iroq qiling.
      </div>
    </div>
  </div>

  <div class="app" id="app">
    <aside class="sidebar" id="sidebar" aria-label="Bosh sahifa menyusi">
      <div class="logo">Fermerlik Darslari</div>
      <p style="margin:0 0 8px 0;color:rgba(255,255,255,0.9)">Amaliy va nazariy videolar</p>
      <nav aria-label="Kategoriyalar" id="category-nav">
        <a href="#" class="sidebar-link active" data-category="dehqonchilik">Dehqonchilik</a>
        <a href="#" class="sidebar-link" data-category="chorvachilik">Chorvachilik</a>
        <a href="#" class="sidebar-link" data-category="parrandachilik">Parrandachilik</a>
        <a href="#" class="sidebar-link" data-category="bogbonchilik">Bog'bonchilik</a>
      </nav>
    </aside>

    <main class="main" id="main">
      <header class="header">
        <div><strong id="category-title">Kategoriya</strong></div>
        <div class="controls" role="search" aria-label="Videolarni qidirish">
          <input id="search" class="search" placeholder="Video nomi bo'yicha izlash..." aria-label="Qidiruv" />
        </div>
      </header>

      <section>
        <h2 id="section-title">Videolar</h2>
        <div style="margin:10px 0;color:rgba(255,255,255,0.9);font-size:0.95rem" id="status">Yuklanmoqda...</div>
        <div id="video-list" class="video-list" aria-live="polite"></div>
      </section>

    </main>
  </div>

  <!-- Modal for embedded playback (opens inside the page instead of navigating to youtube.com) -->
  <div id="playerModal" class="video-modal" aria-hidden="true">
    <div class="video-modal-content" role="dialog" aria-modal="true" aria-label="Video pleer">
      <button id="modalClose" class="modal-close" aria-label="Yopish">✕</button>
      <div class="video-frame">
        <iframe id="modalIframe" src="" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
      </div>
    </div>
  </div>

  <script>
    (function(){
      // Fallback videos grouped by the requested categories.
      const fallback = {
        "dehqonchilik": [
          { "title": "Dehqonchilik: 1-dars", "link": "https://www.youtube.com/watch?v=gq0gz8LUR2g&t=337s" },
          { "title": "Dehqonchilik: 2-dars", "link": "https://www.youtube.com/watch?v=wCci8fDpnP4" }
        ],
        "chorvachilik": [
          { "title": "Chorvachilik: 1-dars", "link": "https://www.youtube.com/watch?v=qR9JoDxyL5g" },
          { "title": "Chorvachilik: 2-dars", "link": "https://www.youtube.com/watch?v=Wz3G2MAx_rw&t=961s" }
        ],
        "parrandachilik": [
          { "title": "Parrandachilik: 1-dars", "link": "https://www.youtube.com/watch?v=Gyd1zbNn3d4" },
          { "title": "Parrandachilik: 2-dars", "link": "https://www.youtube.com/watch?v=iwPRMuh6flk&t=1510s" }
        ],
        "bogbonchilik": [
          { "title": "Bog'bonchilik: 1-dars", "link": "https://www.youtube.com/watch?v=SLHSuSyKpuM&list=PLLu3bYHAYRdJFWoUcCASaISXromL-uI3N" },
          { "title": "Bog'bonchilik: 2-dars", "link": "https://www.youtube.com/watch?v=lAfvz4gWqE4" }
        ]
      };

      const statusEl = document.getElementById('status');
      let videosData = fallback;

      // Try to fetch videos.json to allow dynamic updates; otherwise use fallback
      fetch('videos.json').then(r => {
        if(!r.ok) throw new Error('No videos.json');
        return r.json();
      }).then(json => {
        videosData = json;
      }).catch(()=> {
        // fallback stays
      }).finally(()=> {
        statusEl.textContent = '';
        init();
      });

      const links = document.querySelectorAll('.sidebar-link');
      const listEl = document.getElementById('video-list');
      const categoryTitle = document.getElementById('category-title');
      const searchEl = document.getElementById('search');

      // Modal elements
      const playerModal = document.getElementById('playerModal');
      const modalIframe = document.getElementById('modalIframe');
      const modalClose = document.getElementById('modalClose');

      function init(){
        links.forEach(link => {
          link.addEventListener('click', (e) => {
            e.preventDefault();
            links.forEach(l=>l.classList.remove('active'));
            link.classList.add('active');
            const cat = link.dataset.category;
            categoryTitle.textContent = link.textContent;
            searchEl.value = '';
            loadVideos(cat);
          });
          link.setAttribute('tabindex','0');
          link.addEventListener('keydown', (e) => { if(e.key==='Enter') link.click(); });
        });

        const firstCategory = links[0]?.dataset.category || 'dehqonchilik';
        categoryTitle.textContent = links[0]?.textContent || 'Kategoriya';
        loadVideos(firstCategory);

        searchEl.addEventListener('input', () => {
          const active = document.querySelector('.sidebar-link.active');
          const cat = active?.dataset.category || firstCategory;
          loadVideos(cat, searchEl.value.trim());
        });

        // modal close handlers
        modalClose.addEventListener('click', closeModal);
        playerModal.addEventListener('click', (e) => {
          // close when clicking outside the content
          if(e.target === playerModal) closeModal();
        });
        document.addEventListener('keydown', (e) => { if(e.key === 'Escape') closeModal(); });
      }

      function loadVideos(category, filter=''){
        const videos = (videosData[category] || []).filter(v => v.title.toLowerCase().includes(filter.toLowerCase()));
        displayVideos(videos, category);
      }

      function youtubeIdFromUrl(url){
        try{
          const u = new URL(url);
          const host = u.hostname.toLowerCase();
          // prefer v param if available
          const v = u.searchParams.get('v');
          if(v) return v;
          if(host.includes('youtu.be')){
            return u.pathname.slice(1);
          }
          if(host.includes('youtube') || host.includes('youtu')){
            // check embed path
            if(u.pathname.startsWith('/embed/')) return u.pathname.split('/embed/')[1];
            const parts = u.pathname.split('/').filter(Boolean);
            const last = parts[parts.length - 1] || '';
            if(last.length >= 6 && last.length <= 64) return last;
          }
        }catch(e){
          return url;
        }
        return null;
      }

      function getThumbnailUrl(videoLink){
        const id = youtubeIdFromUrl(videoLink);
        if(!id) return '';
        return `https://i.ytimg.com/vi/${id}/hqdefault.jpg`;
      }

      function displayVideos(videos){
        listEl.innerHTML = '';
        if(!videos || videos.length === 0){
          listEl.innerHTML = '<p style="color:rgba(255,255,255,0.9)">Bu kategoriyada video yo‘q.</p>';
          return;
        }
        videos.forEach(video => {
          const wrap = document.createElement('article');
          wrap.className = 'video';
          wrap.setAttribute('tabindex','0');

          const title = document.createElement('h3');
          title.textContent = video.title;

          const thumbWrap = document.createElement('div');
          thumbWrap.className = 'thumb';
          thumbWrap.setAttribute('role','button');
          thumbWrap.setAttribute('aria-label','Videoni ochish: ' + video.title);
          thumbWrap.tabIndex = 0;

          const thumbImg = document.createElement('img');
          const thumb = getThumbnailUrl(video.link);
          thumbImg.src = thumb || '';
          thumbImg.alt = video.title + ' — video thumbnail';
          thumbImg.loading = 'lazy';

          const playBtn = document.createElement('div');
          playBtn.className = 'play-btn';
          playBtn.textContent = '▶︎ Play';

          thumbWrap.appendChild(thumbImg);
          thumbWrap.appendChild(playBtn);

          function openVideo(){
            const id = youtubeIdFromUrl(video.link);
            if(!id){
              // if not a youtube link, open in new tab
              window.open(video.link, '_blank', 'noopener');
              return;
            }
            // open modal and set iframe src to embed URL with autoplay
            const embedSrc = `https://www.youtube.com/embed/${id}?autoplay=1&rel=0`;
            modalIframe.src = embedSrc;
            playerModal.classList.add('open');
            playerModal.setAttribute('aria-hidden', 'false');
            // focus close button for accessibility
            modalClose.focus();
          }

          function closeModal(){
            // helper inside scope to ensure proper reference
            modalIframe.src = '';
            playerModal.classList.remove('open');
            playerModal.setAttribute('aria-hidden', 'true');
          }

          // Hook global closeModal reference used above
          // (we also define top-level closeModal below for keyboard/Escape handlers)
          // But ensure each thumbWrap click calls the openVideo declared here.
          thumbWrap.addEventListener('click', openVideo);
          thumbWrap.addEventListener('keydown', (e) => { if(e.key === 'Enter' || e.key === ' ') { e.preventDefault(); openVideo(); } });

          const meta = document.createElement('div');
          meta.className = 'meta';

          const externalLink = document.createElement('a');
          const id = youtubeIdFromUrl(video.link);
          externalLink.href = id ? `https://www.youtube.com/watch?v=${id}` : video.link;
          externalLink.target = '_blank';
          externalLink.rel = 'noopener';
          externalLink.className = 'link';
          externalLink.textContent = 'YouTube’da ochish';

          meta.appendChild(externalLink);

          wrap.appendChild(title);
          wrap.appendChild(thumbWrap);
          wrap.appendChild(meta);

          listEl.appendChild(wrap);
        });
      }

      /* -------------------------
         Call widget behavior
         ------------------------- */
      const callLabel = document.getElementById('callLabel');
      const callPanel = document.getElementById('callPanel');
      const callPanelClose = document.getElementById('callPanelClose');
      const copyBtn = document.getElementById('copyBtn');
      const callButton = document.getElementById('callButton');
      const telLink = document.getElementById('telLink');

      function toggleCallPanel(open){
        const isOpen = typeof open === 'boolean' ? open : !callPanel.classList.contains('open');
        if(isOpen){
          callPanel.classList.add('open');
          callPanel.setAttribute('aria-hidden','false');
          callLabel.setAttribute('aria-expanded','true');
          callButton.setAttribute('aria-expanded','true');
          // focus first actionable element for keyboard users
          copyBtn.focus();
        } else {
          callPanel.classList.remove('open');
          callPanel.setAttribute('aria-hidden','true');
          callLabel.setAttribute('aria-expanded','false');
          callButton.setAttribute('aria-expanded','false');
        }
      }

      callLabel.addEventListener('click', ()=> toggleCallPanel());
      callLabel.addEventListener('keydown', (e)=> { if(e.key === 'Enter' || e.key === ' ') { e.preventDefault(); toggleCallPanel(); }});
      callButton.addEventListener('click', ()=> {
        // open phone dialer on supported devices
        window.location.href = 'tel:+998942586045';
      });

      callPanelClose.addEventListener('click', ()=> toggleCallPanel(false));

      // copy number
      copyBtn.addEventListener('click', () => {
        const tel = '+998 94 258 60 45';
        if(navigator.clipboard && navigator.clipboard.writeText){
          navigator.clipboard.writeText(tel).then(() => {
            showTempMessage('Raqam nusxalandi');
          }).catch(() => {
            showTempMessage('Nusxalash imkoni yo‘q — qo‘lda nusxa oling');
          });
        } else {
          // fallback
          const ta = document.createElement('textarea');
          ta.value = tel;
          document.body.appendChild(ta);
          ta.select();
          try{
            document.execCommand('copy');
            showTempMessage('Raqam nusxalandi');
          }catch(e){
            showTempMessage('Nusxalash imkoni yo‘q — qo‘lda nusxa oling');
          }
          ta.remove();
        }
      });

      // close call panel when clicking outside
      document.addEventListener('click', (e) => {
        const path = e.composedPath ? e.composedPath() : (e.path || []);
        if(!path.includes(document.getElementById('callWidget')) && callPanel.classList.contains('open')){
          toggleCallPanel(false);
        }
      });

      // ESC to close call panel
      document.addEventListener('keydown', (e) => {
        if(e.key === 'Escape') toggleCallPanel(false);
      });

      function showTempMessage(msg, ms = 2000){
        // tiny ephemeral message near the call widget
        const el = document.createElement('div');
        el.textContent = msg;
        el.style.position = 'fixed';
        el.style.right = '18px';
        el.style.top = '86px';
        el.style.background = 'rgba(0,0,0,0.75)';
        el.style.color = '#fff';
        el.style.padding = '8px 12px';
        el.style.borderRadius = '8px';
        el.style.zIndex = 90;
        document.body.appendChild(el);
        setTimeout(()=> el.remove(), ms);
      }

      // Top-level closeModal used for modal keyboard handling
      function closeModal(){
        modalIframe.src = '';
        playerModal.classList.remove('open');
        playerModal.setAttribute('aria-hidden', 'true');
      }

      // ensure modalClose works (also attached inside init)
      modalClose.addEventListener('click', closeModal);

    })();
  </script>
</body>
</html>
```
