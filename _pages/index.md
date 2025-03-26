---
layout: page
title: Home
id: home
permalink: /
---

<button id="toggle-dark-mode">🌙 다크 모드</button>

<script>
  const toggleButton = document.getElementById('toggle-dark-mode');
  toggleButton.addEventListener('click', function () {
    document.body.classList.toggle('dark-mode');
  });
</script>

# Welcome! 🌱

<p style="padding: 3em 1em; background: #f5f7ff; border-radius: 4px;">
  Take a look at <span style="font-weight: bold">[[Your first note]]</span> to get started on your exploration.
</p>

This digital garden template is free, open-source, and [available on GitHub here](https://github.com/maximevaillancourt/digital-garden-jekyll-template).

The easiest way to get started is to read this [step-by-step guide explaining how to set this up from scratch](https://maximevaillancourt.com/blog/setting-up-your-own-digital-garden-with-jekyll).

<strong>Recently updated notes</strong>

<ul>
  {% assign recent_notes = site.notes | sort: "last_modified_at_timestamp" | reverse %}
  {% for note in recent_notes limit: 5 %}
    <li>
      {{ note.last_modified_at | date: "%Y-%m-%d" }} — <a class="internal-link" href="{{ site.baseurl }}{{ note.url }}">{{ note.title }}</a>
    </li>
  {% endfor %}
</ul>

<div class="recent-notes">
  {% assign recent_notes = site.notes | sort: "last_modified_at_timestamp" | reverse %}
  {% for note in recent_notes limit: 5 %}
    <div class="note-card">
      <span class="note-date">{{ note.last_modified_at | date: "%Y-%m-%d" }}</span>
      <a class="internal-link" href="{{ site.baseurl }}{{ note.url }}">{{ note.title }}</a>
    </div>
  {% endfor %}
</div>

<style>
  .wrapper {
    max-width: 46em;
  }

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
  }

  .note-date {
    font-size: 0.9em;
    color: gray;
  }
  .dark-mode .note-card {
  background: #2a2a2a;
  box-shadow: none;
  }
  body.dark-mode {
  background-color: #1e1e1e;
  color: #ffffff;
}

.dark-mode a {
  color: #4dabf7;
}
</style>
