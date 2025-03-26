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
    display: flex;
    flex-wrap: wrap;
    gap: 16px;
    justify-content: center;
  }

  .note-card {
    background: #ffffff;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 2px 4px 10px rgba(0, 0, 0, 0.1);
    transition: transform 0.2s ease-in-out;
    width: 100%;
    max-width: 500px;
  }

  .note-card:hover {
    transform: scale(1.02);
  }

  /* 제목 스타일 */
  .note-title {
    font-size: 1.5em;
    font-weight: bold;
    margin-bottom: 10px;
  }

  .note-title a {
    text-decoration: none;
    color: #333;
  }

  .note-title a:hover {
    color: #007bff;
  }

  /* 내용 스타일 (4줄 이후 ... 표시) */
  .note-content {
    font-size: 1em;
    color: #555;
    line-height: 1.5;
    max-height: 6em;
    overflow: hidden;
    display: -webkit-box;
    -webkit-line-clamp: 4;
    -webkit-box-orient: vertical;
    text-overflow: ellipsis;
    margin-bottom: 10px;
  }

  /* 날짜 스타일 */
  .note-date {
    font-size: 0.9em;
    color: #888;
    margin-bottom: 10px;
  }

  /* 태그 스타일 */
  .note-tags {
    margin-top: 10px;
  }

  .tag {
    display: inline-block;
    background: #007bff;
    color: #fff;
    padding: 5px 10px;
    font-size: 0.8em;
    border-radius: 5px;
    margin-right: 5px;
  }
</style>
