<!-- @format -->

# Important Jinja

Jinja Special placeholders

## How to check if user is authenticated in jinja to template conditions

```bash
{% if request.user.is_authenticated %}
    <p>Hello</p>
{% endif %}
```

## Jinja if else

```bash
{% if "new" in res.status %}
    <p>Status: {{res.status}} </td>
{% else %}
     <p>Status: Old </td>
{% endif %}
```
