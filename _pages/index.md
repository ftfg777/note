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
      <!-- 제목 -->
      <h2 class="note-title">
        <a href="{{ site.baseurl }}{{ note.url }}">{{ note.title }}</a>
      </h2>

      <!-- 내용 (4줄까지만 보이고 그 이후는 ...) -->
      <p class="note-content">
        {{ note.content | strip_html | truncatewords: 40, "..." }}
      </p>

      <!-- 작성 날짜 -->
      <p class="note-date">
        📅 {{ note.last_modified_at | date: "%Y-%m-%d" }}
      </p>

      <!-- 태그 -->
      {% if note.tags %}
        <div class="note-tags">
          {% for tag in note.tags %}
            <span class="tag">{{ tag }}</span>
          {% endfor %}
        </div>
      {% endif %}
    </div>

{% endfor %}

</div>

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
    margin-bottom: 20px;
  }

  /* 최근 노트 리스트 */
.recent-notes {
  margin-top: 20px;
  display: grid;
  grid-template-columns: repeat(3, 1fr); /* 한 줄에 3개 */
  gap: 15px;
  justify-content: center;
}

/* 카드 스타일 */
.note-card {
  background: #ffffff;
  border-radius: 8px;
  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
  padding: 15px;
  transition: transform 0.2s ease-in-out;
  display: flex;
  flex-direction: column;
  height: 230px; /* 높이 고정 */
}

.note-card:hover {
  transform: scale(1.03);
}

/* 제목 스타일 */
.note-title {
  font-size: 1.2em;
  font-weight: bold;
  margin-bottom: 8px;
}

.note-title a {
  text-decoration: none;
  color: #333;
}

.note-title a:hover {
  color: #007bff;
}

/* 내용 스타일 */
.note-content {
  font-size: 0.9em;
  color: #555;
  line-height: 1.5;
  max-height: 4.5em;
  overflow: hidden;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  text-overflow: ellipsis;
  flex-grow: 1; /* 남는 공간 차지 */
}

/* 날짜 스타일 (하단 고정) */
.note-date {
  font-size: 0.8em;
  color: #888;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  margin-top: auto;
}

/* 날짜 아이콘 */
.note-date-icon {
  font-size: 0.9em; /* 아이콘 크기 살짝 줄임 */
  margin-right: 5px;
}

/* 태그 스타일 */
.note-tags {
  margin-top: 8px;
}

.tag {
  display: inline-block;
  background: #007bff;
  color: #fff;
  padding: 4px 8px;
  font-size: 0.7em;
  border-radius: 5px;
  margin-right: 4px;
}
</style>
