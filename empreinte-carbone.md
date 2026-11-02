---
title: "Empreinte carbone de mes recherches"
permalink: "/empreinte-carbone/"
layout: "single"
author_profile: true
---

Je suis avec cette page les émissions liées à mon travail de recherche : le calcul (entraînement et inférence de modèles) et les déplacements en conférence. Les chiffres sont en kg CO₂e et mis à jour au fil de l’eau.

## Déplacements en conférence

{% assign total_travel = 0.0 %}
<div style="overflow-x:auto"><table>
<thead><tr><th>Date</th><th>Événement</th><th>Trajet</th><th>Mode</th><th>km</th><th>kg CO₂e</th></tr></thead>
<tbody>
{% for t in site.data.carbon_travel %}{% assign v = t.kg_co2e | default: 0 %}{% assign total_travel = total_travel | plus: v %}<tr><td>{{ t.date }}</td><td>{{ t.event }}</td><td>{{ t.from_to }}</td><td>{{ t.mode }}</td><td>{{ t.km }}</td><td>{% if t.kg_co2e %}{{ t.kg_co2e }}{% else %}à compléter{% endif %}</td></tr>
{% endfor %}
</tbody>
<tfoot><tr><th colspan="5">Total déplacements</th><th>{{ total_travel }}</th></tr></tfoot>
</table></div>

## Calcul

{% assign total_compute = 0.0 %}
<div style="overflow-x:auto"><table>
<thead><tr><th>Projet</th><th>Outil</th><th>Matériel</th><th>Heures</th><th>kWh</th><th>kg CO₂e</th></tr></thead>
<tbody>
{% for c in site.data.carbon_compute %}{% assign v = c.kg_co2e | default: 0 %}{% assign total_compute = total_compute | plus: v %}<tr><td>{{ c.project }}</td><td>{{ c.tool }}</td><td>{{ c.hardware }}</td><td>{{ c.hours }}</td><td>{{ c.kwh }}</td><td>{% if c.kg_co2e %}{{ c.kg_co2e }}{% else %}à compléter{% endif %}</td></tr>
{% endfor %}
</tbody>
<tfoot><tr><th colspan="5">Total calcul</th><th>{{ total_compute }}</th></tr></tfoot>
</table></div>

## Total

**{{ total_travel | plus: total_compute }} kg CO₂e** déclarés à ce jour (hors lignes marquées « à compléter »).

## Méthode

Pour le calcul, je mesure la consommation avec des outils comme CodeCarbon ou Green Algorithms, puis je convertis en CO₂e avec l’intensité carbone du réseau électrique utilisé. Pour les déplacements, j’utilise les facteurs d’émission de la Base Empreinte de l’ADEME (ou le simulateur impactco2.fr), par mode de transport. Les données brutes sont dans les fichiers `_data/carbon_travel.yml` et `_data/carbon_compute.yml` de ce dépôt.
