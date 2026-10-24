{{- $name := replaceRE `^\d{4}-\d{2}-\d{2}-` "" .File.ContentBaseName -}}
---
title: "{{ replace $name "-" " " | title }}"
date: {{ .Date }}
slug: "{{ $name }}"
categories: []
tags: []
draft: true
---
