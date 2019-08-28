<div class="panel panel-primary">
<div class="panel-heading">
<span class="panel-title"><strong>Important Dates</strong></span>
</div>
<ul class="list-group">
{% for date in site.data.dates %}
{% unless date.hide_from contains "website" %}
{% if date.expired %}
<li class="list-group-item alert-danger">
  <div style="margin-left:18px">
  <div style="margin-left:-18px" class="glyphicon glyphicon-check float-left"> </div>
{% else %}
<li class="list-group-item alert-success">
  <div style="margin-left:18px">
  <div style="margin-left:-18px" class="glyphicon glyphicon-unchecked float-left"> </div>
{% endif %}
{% if date.entries %}
  {% for entry in date.entries %}
    {% if entry.date %}
      {% capture t %} 
      <time datetime="{{entry.date}}">
        {{ entry.date | date: "%a %d %b %Y"}}
      </time>
      {% endcapture %}
    {% elsif entry.to and entry.from %}
      {% capture t %} 
        {% capture from %}
          {% assign fy = entry.from | date: "%Y" %}
          {% assign ty = entry.to 	| date: "%Y" %}
          {% assign fm = entry.from | date: "%b" %}
          {% assign tm = entry.to 	| date: "%b" %}
          {% if fy != ty %}
            {{ entry.from | date: "%a %d %b %Y" }}
          {% elsif fm != tm %}
            {{ entry.from | date: "%a %d %b" }}
          {% else %}
            {{ entry.from | date: "%a %d" }}
          {% endif %}
        {% endcapture %}
        <time datetime="{{entry.from}}">{{ from }}</time> - 
        <time datetime="{{entry.to}}">{{ entry.to | date: "%a %d %b %Y"}}</time>
      {% endcapture %}
    {% endif %}
    <span>{% if forloop.first %}
      {{ t }}
      {% if entry.zone %}
        <span data-toggle="tooltip" title="Timezone: {{ entry.zone.label }}">
        <span class="glyphicon glyphicon-time"></span>
        </span>
      {% endif %}
    {% else %}
    <strike>{{ t }}</strike>
    {% endif %}</span>
  {% endfor %}
{% else %}
  <span>TBD</span>
{% endif %}
<br><span>{{ date.summary.website | default: date.summary }}</span>
</div>
</li>
{% endunless %}
{% endfor %}
<li class="list-group-item">
<a target="_blank" href="/important-dates.ics" title="Save important dates">
<div style="margin-left:18px">
<div style="margin-left:-18px" class="glyphicon glyphicon-calendar float-left"></div>
<span>Add to your calendar (*.ics)</span></div></a>
</li>
</ul>
</div>

<style>
 .vcenter { 
  display: inline-block;
  vertical-align: middle;
  float: none;
}
</style>

<div class="panel panel-primary">
<div class="panel-heading">
<strong>Sponsors & Supporters</strong>
</div>
<ul class="list-group">
{% for supporter in site.data.supporters %}
<li class="list-group-item">
  <div class="row">
  <div class="col-xs-offset-3 col-xs-6"><a href="{{ supporter.link }}"><img style="max-height:100px;" class="img-responsive center-block" src="{{ supporter.logo }}" alt="{{supporter.name}}"></a></div><div class="col-sm-4 col-md-3 text-center text-muted vcenter">{% if supporter.tier %}{{supporter.tier | capitalize }} {% endif%}{{supporter.type}}</div>
  </div>
</li>
{% endfor %}
</ul>
</div>

<script>
$(document).ready(function(){$('[data-toggle="tooltip"]').tooltip();});
</script>