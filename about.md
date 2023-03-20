---
layout: page
title: About
permalink: /about/
---

### Interesting Deets

  - born in Philadelphia, Woodford was born in Virginia
  - golf is life and life is golf
  - enjoy hiking parks & traveling with my wife
  - love the process of a good cup of coffee
  - fixing up my house & working on tech / software during the week
 
### Current Show & Movie Watchlist

<table style="margin: 20px;">
  {% for row in site.data.movies %}
    {% if forloop.first %}
      <tr>
        {% for pair in row %}
          <th>{{ pair[0] }}</th>
        {% endfor %}
      </tr>
    {% endif %}
    {% tablerow pair in row %}
      {{ pair[1] }}
    {% endtablerow %}
  {% endfor %}
</table>
