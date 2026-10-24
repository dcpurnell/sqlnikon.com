{{- $name := replaceRE `^\d{4}-\d{2}-\d{2}-` "" .File.ContentBaseName -}}
---
title: "{{ replace $name "-" " " | title }}"
date: {{ .Date }}
location: ""
gallery: "https://sqlnikon.smugmug.com/"
cover:
  image: ""
draft: true
---

A few words about the walk.

<!-- Photos: resize to ~1600px, strip metadata (exiftool -all= photo.jpg), put them
     in static/photography/<this-file-name>/, and list them in a gallery: -->
<div class="gallery">
<a href="/photography/{{ .File.ContentBaseName }}/1.jpg"><img src="/photography/{{ .File.ContentBaseName }}/1.jpg" alt="" loading="lazy"></a>
</div>

[See the full gallery on SmugMug]({{ "{{" }}< param gallery >{{ "}}" }})
