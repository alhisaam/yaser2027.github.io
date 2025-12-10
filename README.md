[<!doctype html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>منصة الوسائط — الإصدار المتكامل</title>
  <style>
    body{font-family:Tahoma, Arial, sans-serif; margin:0; background:#1b1b1b; color:#fff;}
    header{background:#000; color:#fff; padding:25px; text-align:center; font-size:1.8rem; box-shadow:0 2px 10px rgba(0,0,0,0.5);}    
    nav{text-align:center; padding:15px; background:#111; display:flex; justify-content:center; gap:20px;}
    nav a{color:#fff; text-decoration:none; font-size:1.1rem; padding:8px 16px; border-radius:8px; background:#222; transition:0.3s;}
    nav a:hover{background:#444;}

    .section{padding:30px; max-width:1300px; margin:auto;}
    h2{margin-bottom:20px; font-size:1.6rem;}

    /* Gallery */
    .gallery{display:grid; grid-template-columns:repeat(auto-fill,minmax(230px,1fr)); gap:18px;}
    .gallery img{width:100%; border-radius:12px; cursor:pointer; transition:0.3s; box-shadow:0 4px 10px rgba(0,0,0,0.4);}    
    .gallery img:hover{transform:scale(1.05);}    

    /* Image Viewer */
    #viewer{display:none; position:fixed; inset:0; background:rgba(0,0,0,0.9); justify-content:center; align-items:center; z-index:999;}    
    #viewer img{max-width:90%; max-height:90%; border-radius:12px;}

    /* Audio */
    .audio-box{background:#222; padding:20px; border-radius:12px; box-shadow:0 4px 15px rgba(0,0,0,0.4);}    
    .audio-list{display:flex; flex-direction:column; gap:20px;}
    audio{width:100%;}

    /* File Upload */
    .upload-box{background:#222; padding:25px; border-radius:12px; box-shadow:0 4px 15px rgba(0,0,0,0.4); margin-bottom:30px;}
    input[type="file"]{background:#333; color:#fff; padding:10px; border-radius:8px; border:none;}

    /* Categories */
    .categories{display:flex; gap:15px; margin-bottom:20px;}
    .categories button{background:#333; color:#fff; padding:10px 18px; border:none; border-radius:10px; cursor:pointer; transition:0.3s;}
    .categories button:hover{background:#555;}

    footer{text-align:center; padding:20px; background:#000; color:#ddd; margin-top:40px; font-size:0.9rem;}
  </style>
</head>
<body>
  <header>منصة الوسائط — النسخة الكاملة المتطورة</header>

  <!-- شريط صفحات -->
  <nav>
    <a href="#images">الصور</a>
    <a href="#audio">الصوتيات</a>
    <a href="#upload">رفع الملفات</a>
    <a href="#about">عن المنصة</a>
  </nav>

  <!-- رفع الملفات -->
  <div class="section" id="upload">
    <h2>رفع الصور والصوتيات</h2>
    <div class="upload-box">
      <p>يمكنك رفع صورة أو ملف صوتي ليظهر مباشرة في المنصة:</p>
      <input type="file" id="fileInput" accept="image/*, audio/*" onchange="handleUpload(event)">
    </div>
  </div>

  <!-- الصور -->
  <div class="section" id="images">
    <h2>معرض الصور</h2>

    <div class="categories">
      <button onclick="filterImages('all')">الكل</button>
      <button onclick="filterImages('nature')">طبيعة</button>
      <button onclick="filterImages('work')">عمل</button>
      <button onclick="filterImages('people')">شخصيات</button>
    </div>

    <div class="gallery" id="gallery">
      <img data-cat="nature" src="https://via.placeholder.com/400x250?text=طبيعة+1" onclick="openViewer(this.src)">
      <img data-cat="work" src="https://via.placeholder.com/400x250?text=عمل+1" onclick="openViewer(this.src)">
      <img data-cat="people" src="https://via.placeholder.com/400x250?text=شخصيات+1" onclick="openViewer(this.src)">
      <img data-cat="nature" src="https://via.placeholder.com/400x250?text=طبيعة+2" onclick="openViewer(this.src)">
    </div>
  </div>

  <!-- عارض الصور -->
  <div id="viewer" onclick="closeViewer()">
    <img id="viewer-img" src="">
  </div>

  <!-- الصوت -->
  <div class="section" id="audio">
    <h2>الصوتيات</h2>
    <div class="audio-box">
      <div class="audio-list" id="audioList">
        <audio controls><source src="audio1.mp3" type="audio/mpeg"></audio>
        <audio controls><source src="audio2.mp3" type="audio/mpeg"></audio>
      </div>
    </div>
  </div>

  <!-- معلومات -->
  <div class="section" id="about">
    <h2>عن المنصة</h2>
    <p>هذه نسخة متقدمة من منصة الوسائط تدعم: رفع الملفات، تصنيف الصور، معرض احترافي، تشغيل صوت، تكبير الصور، وتنظيم كامل للصفحات.</p>
  </div>

  <footer>© 2025 — منصة الوسائط المتطورة</footer>

  <script>
    function openViewer(src){
      document.getElementById('viewer-img').src = src;
      document.getElementById('viewer').style.display = 'flex';
    }
    function closeViewer(){
      document.getElementById('viewer').style.display = 'none';
    }

    function filterImages(category){
      let imgs = document.querySelectorAll('#gallery img');
      imgs.forEach(img => {
        img.style.display = (category === 'all' || img.dataset.cat === category) ? 'block' : 'none';
      });
    }

    function handleUpload(event){
      const file = event.target.files[0];
      if(!file) return;

      const url = URL.createObjectURL(file);
      if(file.type.startsWith('image')){
        const img = document.createElement('img');
        img.src = url;
        img.style.cursor = 'pointer';
        img.onclick = () => openViewer(url);
        document.getElementById('gallery').appendChild(img);
      }
      else if(file.type.startsWith('audio')){
        const audio = document.createElement('audio');
        audio.controls = true;
        audio.innerHTML = `<source src="${url}" type="audio/mpeg">`;
        document.getElementById('audioList').appendChild(audio);
      }
    }
  </script>
</body>
</html>
](https://github.com/alhisaam/yaser2027.github.io)
