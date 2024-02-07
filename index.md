---
title: Online gehostete Anweisungen
permalink: index.html
layout: home
---

# Inhaltsverzeichnis

Links zu jeder Fallstudie sind unten aufgeführt.


## Fallstudien wurden für die Inhaltsaktualisierung vom Mai 2023 neu organisiert

{% assign casestudy= site.pages | where_exp:"page", "page.url contains '/Instructions/CaseStudyv2/'" %}
| Modul | Fallstudie |
| --- | --- | 
{% for activity in casestudy  %}| {{ activity.casestudy.module }} | [{{ activity.casestudy.title }}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}


## Alte Fallstudienorganisation

{% assign casestudy= site.pages | where_exp:"page", "page.url contains '/Instructions/CaseStudy/'" %}
| Modul | Fallstudie |
| --- | --- | 
{% for activity in casestudy  %}| {{ activity.casestudy.module }} | [{{ activity.casestudy.title }}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}