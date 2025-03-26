---
layout: page
title: Home
id: home
permalink: /
---

# Welcome! 🌱

<div class="welcome-card">
  <h1>반갑습니다 👋</h1>
  <p>이런 누추한 곳에 오시다니 환영합니다</p>
  <p>시작하려면 <strong>[[Your first note]]</strong>를 확인해봐!</p>
</div>

<strong>📌 최근 업데이트된 노트</strong>

<div class="recent-notes">
  {% assign recent_notes = site.notes | sort: "last_modified_at_timestamp" | reverse %}
  {% for note in recent_notes limit: 5 %}
    <div class="note-card">
     <pre>{{ note | inspect }}</pre>
      <span class="note-date">{{ note.last_modified_at | date: "%Y-%m-%d" }}</span>
      <a class="internal-link" href="{{ site.baseurl }}{{ note.url }}">{{ note.title }}</a>
    </div>
  {% endfor %}
</div>

<button id="toggle-dark-mode">🌙 다크 모드</button>

<style>
  /* 기본 스타일 */
  body {
    font-family: 'Inter', sans-serif;
    background-color: #fdfdfd;
    color: #333;
    line-height: 1.6;
    padding: 20px;
  }

  h1 {
    color: #2a7ae2;
    text-align: center;
  }

  /* 환영 메시지 카드 */
  .welcome-card {
    background: linear-gradient(135deg, #eef2ff, #c7d2fe);
    padding: 2em;
    border-radius: 8px;
    text-align: center;
    box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.1);
  }

  /* 최근 노트 리스트 */
  .recent-notes {
    margin-top: 20px;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 12px;
  }

  .note-card {
    background: #ffffff;
    padding: 15px;
    border-radius: 8px;
    box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.1);
    transition: transform 0.2s ease-in-out;
  }

  .note-card:hover {
    transform: scale(1.03);
  }

  .note-date {
    font-size: 0.9em;
    color: gray;
  }

  /* 버튼 스타일 */
  #toggle-dark-mode {
    margin-top: 20px;
    padding: 10px 15px;
    border: none;
    background-color: #007acc;
    color: white;
    border-radius: 5px;
    cursor: pointer;
  }

  #toggle-dark-mode:hover {
    background-color: #005f99;
  }

  /* 다크 모드 스타일 */
  body.dark-mode {
    background-color: #1e1e1e;
    color: #ffffff;
  }

  .dark-mode a {
    color: #4dabf7;
  }

  .dark-mode .note-card {
    background: #2a2a2a;
    box-shadow: none;
  }

  .dark-mode #toggle-dark-mode {
    background-color: #facc15;
    color: black;
  }
</style>

<script>
  const toggleButton = document.getElementById('toggle-dark-mode');
  toggleButton.addEventListener('click', function () {
    document.body.classList.toggle('dark-mode');
  });
</script>
