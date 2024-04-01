{% for image in site.static_files %}
{% if image.path contains '/Go-Logo_Blue.svg' %}
<img src="{{site.baseurl}}{{image.path}}" width="80" height="70.8" alt="Go logo" style="display: block; margin: 0 auto">
{% endif %}
{% endfor %}
