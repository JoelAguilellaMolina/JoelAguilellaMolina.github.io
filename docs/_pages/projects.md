---
title:
layout: default
permalink: /projects/
published: true
---


<div class="ProjectContainer">

	<div class="gallery">

  {% for project in site.projects %}

  {% assign bg_image = project.tile_image | default: "/assets/images/IconJust5Minutes.png" %}

  {% if project.redirect %}

  <div class="projectTile" style="background-image: url('{{ bg_image }}')">
          <a href="{{ project.redirect }}" target="_blank">
          <span>
              <h2>{{ project.title }}</h2>
              <br/>
              <p>{{ project.description }}</p>
          </span>
          </a>
  </div>

  {% else %}

  <div class="projectTile" style="background-image: url('{{ bg_image }}')">
          <a href="{{ project.url | prepend: site.baseurl | prepend: site.url }}">
          <span>
              <h2>{{ project.title }}</h2>
              <br/>
              <p>{{ project.description }}</p>
          </span>
          </a>
  </div>

  
  

  {% endif %}

  {% endfor %}


	</div>

</div>
