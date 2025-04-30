# test

コンテンツ内容を全て書き出してくれるはず

{% if site.contents %}
{% assign doclist = site.static_files | sort: 'url' %}
{% for doc in doclist %}

- [{{ doc.name }}]({{ site.baseurl }}{{ doc.url }})
{% endfor %}
{% endif %}
