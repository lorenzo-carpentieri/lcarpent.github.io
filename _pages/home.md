---
title: "UNISA HPC - Publications"
layout: gridlay
excerpt: "UNISA HPC: Publications."
sitemap: false
permalink: /
---

## Welcome to the HPC Team @ ISISLab

We are team of the [ISISLab](https://www.isislab.it/), based at the [University of Salerno](https://www.unisa.it).
Our interests span from high-level programming models for HPC and embedded systems, to energy-efficient computing and performance optimization on various layers of the HPC stack.

## Our projects

{% assign number_printed = 0 %}
{% for publi in site.data.projects %}

{% assign even_odd = number_printed | modulo: 2 %}
{% if publi.highlight == 1 %}

{% if even_odd == 0 %}
<div class="row">
{% endif %}

<div class="col-sm-6 clearfix">
 <div class="well">
  <b><a href="{{ site.url }}{{ site.baseurl }}/{{ publi.sitelink }}">{{ publi.title }}</a></b>
  <img src="{{ site.url }}{{ site.baseurl }}/images/pubpic/{{ publi.image }}" class="img-responsive" width="33%" style="float: left" />
  <p>{{ publi.description }}</p>
  <p><strong>Published at: <a href="{{ publi.publink.url }}">{{ publi.publink.display }}</a></strong></p>
  <p class="text-danger"><strong> {{ publi.news1 }}</strong></p>
  <p> {{ publi.news2 }}</p>
 </div>
</div>

{% assign number_printed = number_printed | plus: 1 %}

{% if even_odd == 1 %}
</div>
{% endif %}

{% endif %}
{% endfor %}

{% assign even_odd = number_printed | modulo: 2 %}
{% if even_odd == 1 %}
</div>
{% endif %}

<p> &nbsp; </p>
