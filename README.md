# dynamic-type-and-or-query-in-django
dynamic type and or query in django

``` python
# Inputs Are
# >>> values = ['yogesh',56]
# >>> types=['exact','lte']
# >>> operator = ['and','or']
# >>> fields=['first_name','price']
# >>> dynamic_query(fields, types, values, operator)

def dynamic_query(fields, types, values, operator):
    from django.db.models import Q
    queries = []
    for (f, t, v) in zip(fields, types, values):
    if v != "":
        kwargs = {str('%s__%s' % (f,t)) : str('%s' % v)}
        queries.append(Q(**kwargs))
    if queries:
        q = Q()
        for i, query in enumerate(queries):
            if operator[i] == "and":
                q = q & query
            elif operator[i] == "or":
                q = q | query
            else:
                q = None
        if q:
            return q
    else:
        return {}
```
