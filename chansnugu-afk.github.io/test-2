class-site/
 ├─ index.html
 <!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>우리 반 학급 사이트</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <header>
    <h1>🏫 우리 반 학급 사이트</h1>
    <p>함께 만드는 즐거운 학급 공간</p>
  </header>

  <nav>
    <a href="#notice">알림판</a>
    <a href="#board">자유게시판</a>
    <a href="#gallery">추억 갤러리</a>
  </nav>

  <!-- 알림판 -->
  <section id="notice">
    <h2>📢 알림판</h2>

    <div class="input-box">
      <input type="text" id="noticeInput" placeholder="알림 내용을 입력하세요">
      <button onclick="addNotice()">등록</button>
    </div>

    <ul id="noticeList"></ul>
  </section>

  <!-- 자유게시판 -->
  <section id="board">
    <h2>💬 자유게시판</h2>

    <div class="input-box">
      <input type="text" id="boardWriter" placeholder="이름">
      <input type="text" id="boardInput" placeholder="글 내용을 입력하세요">
      <button onclick="addBoardPost()">작성</button>
    </div>

    <div id="boardList"></div>
  </section>

  <!-- 갤러리 -->
  <section id="gallery">
    <h2>📸 추억 갤러리</h2>

    <div class="input-box">
      <input type="file" id="imageUpload" accept="image/*">
      <button onclick="uploadImage()">사진 올리기</button>
    </div>

    <div id="galleryList" class="gallery-grid"></div>
  </section>

  <footer>
    <p>© 2026 우리 반 학급 사이트</p>
  </footer>

  <script src="script.js"></script>
</body>
</html>
 ├─ style.css
 body {
  margin: 0;
  font-family: "Pretendard", sans-serif;
  background: #f5f7fb;
  color: #333;
}

header {
  background: #4a90e2;
  color: white;
  text-align: center;
  padding: 30px;
}

nav {
  background: #357abd;
  padding: 12px;
  text-align: center;
}

nav a {
  color: white;
  text-decoration: none;
  margin: 0 15px;
  font-weight: bold;
}

section {
  background: white;
  margin: 20px auto;
  padding: 20px;
  width: 90%;
  max-width: 900px;
  border-radius: 12px;
  box-shadow: 0 2px 10px rgba(0,0,0,0.1);
}

h2 {
  margin-top: 0;
}

.input-box {
  margin-bottom: 15px;
}

input[type="text"] {
  width: 70%;
  padding: 10px;
  margin: 5px;
}

button {
  padding: 10px 15px;
  background: #4a90e2;
  border: none;
  color: white;
  border-radius: 6px;
  cursor: pointer;
}

button:hover {
  background: #357abd;
}

ul {
  padding-left: 20px;
}

.post {
  border-bottom: 1px solid #ddd;
  padding: 10px 0;
}

.gallery-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 15px;
}

.gallery-grid img {
  width: 100%;
  border-radius: 10px;
  object-fit: cover;
}

footer {
  text-align: center;
  padding: 20px;
  color: gray;
}
 └─ script.js
 // =====================
// 알림판
// =====================

let notices = JSON.parse(localStorage.getItem("notices")) || [];

function renderNotices() {
  const list = document.getElementById("noticeList");
  list.innerHTML = "";

  notices.forEach((notice, index) => {
    const li = document.createElement("li");
    li.innerHTML = `
      ${notice}
      <button onclick="deleteNotice(${index})">삭제</button>
    `;
    list.appendChild(li);
  });
}

function addNotice() {
  const input = document.getElementById("noticeInput");

  if (input.value.trim() === "") return;

  notices.push(input.value);
  localStorage.setItem("notices", JSON.stringify(notices));

  input.value = "";
  renderNotices();
}

function deleteNotice(index) {
  notices.splice(index, 1);
  localStorage.setItem("notices", JSON.stringify(notices));
  renderNotices();
}

// =====================
// 자유게시판
// =====================

let posts = JSON.parse(localStorage.getItem("posts")) || [];

function renderPosts() {
  const boardList = document.getElementById("boardList");
  boardList.innerHTML = "";

  posts.forEach((post, index) => {
    const div = document.createElement("div");
    div.className = "post";

    div.innerHTML = `
      <strong>${post.writer}</strong><br>
      ${post.content}<br>
      <button onclick="deletePost(${index})">삭제</button>
    `;

    boardList.appendChild(div);
  });
}

function addBoardPost() {
  const writer = document.getElementById("boardWriter");
  const content = document.getElementById("boardInput");

  if (
    writer.value.trim() === "" ||
    content.value.trim() === ""
  ) return;

  posts.push({
    writer: writer.value,
    content: content.value
  });

  localStorage.setItem("posts", JSON.stringify(posts));

  writer.value = "";
  content.value = "";

  renderPosts();
}

function deletePost(index) {
  posts.splice(index, 1);
  localStorage.setItem("posts", JSON.stringify(posts));
  renderPosts();
}

// =====================
// 갤러리
// =====================

let images = JSON.parse(localStorage.getItem("images")) || [];

function renderGallery() {
  const gallery = document.getElementById("galleryList");
  gallery.innerHTML = "";

  images.forEach((src, index) => {
    const div = document.createElement("div");

    div.innerHTML = `
      <img src="${src}">
      <button onclick="deleteImage(${index})">삭제</button>
    `;

    gallery.appendChild(div);
  });
}

function uploadImage() {
  const fileInput = document.getElementById("imageUpload");

  const file = fileInput.files[0];

  if (!file) return;

  const reader = new FileReader();

  reader.onload = function(e) {
    images.push(e.target.result);

    localStorage.setItem("images", JSON.stringify(images));

    renderGallery();
  };

  reader.readAsDataURL(file);
}

function deleteImage(index) {
  images.splice(index, 1);

  localStorage.setItem("images", JSON.stringify(images));

  renderGallery();
}

// =====================
// 시작 시 불러오기
// =====================

renderNotices();
renderPosts();
renderGallery();
