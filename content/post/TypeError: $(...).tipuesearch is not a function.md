{
    "date": "2015-03-13",
    "description": null,
    "draft": false,
    "id": 7,
    "image": null,
    "meta_title": null,
    "slug": "typeerror-tipuesearch-is-not-a-function",
    "tags": [
        "admins"
    ],
    "title": "TypeError: $(...).tipuesearch is not a function",
    "type": "post"
}


Решение:

Устанавливаем поиск по инструкции с сайта http://www.tipue.com/search/docs/. Но! Функция показа результатов должна быть такой:

```
<script>
var $j = jQuery.noConflict();
$j(document).ready(function() {
     $j('#tipue_search_input').tipuesearch({
         'show': 10,
         'mode': 'json',
         'contentLocation': '{{ SITEURL }}/tipuesearch_content.json'
     });
});
</script>
```
