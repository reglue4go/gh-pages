<!DOCTYPE html>
<html lang="{{ page.lang | default: site.lang | default: 'en-US' }}">
  <head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">

{% seo %}

<link rel="stylesheet" href="{{ '/assets/css/style.css?v=' | append: site.github.build_revision | relative_url }}">
{% include head-custom.html %}

{% for image in site.static_files %}
{% if image.path contains '/Go-Logo_Blue.svg' %}

<link rel="icon" href="{{site.baseurl}}{{image.path}}" sizes="any" type="image/svg+xml">
{% endif %}
{% endfor %}

<!-- custom styles -->

<!-- <link rel="stylesheet" href="{{ '/_assets/css/app.css?v=' | append: site.github.build_revision | relative_url  }}"> -->

  </head>
  <body>
    <div class="container-lg px-3 my-5 markdown-body">
      {% if site.title and site.title != page.title %}
      <h1><a href="{{ "/" | absolute_url }}">{{ site.title }}</a></h1>
      {% endif %}

      {{ content }}

      {% if site.github.private != true and site.github.license %}
      <div class="footer border-top border-gray-light mt-5 pt-3 text-right text-gray">
        This site is open source. {% github_edit_link "Improve this page" %}.
      </div>
      {% endif %}

      {% include footGologo.md %}
    </div>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/anchor-js/4.1.0/anchor.min.js" integrity="sha256-lZaRhKri35AyJSypXXs4o6OPFTbTmUoltBbDCbdzegg=" crossorigin="anonymous"></script>
    <script>anchors.add();</script>

  </body>
</html>
