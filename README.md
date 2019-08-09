### voluptuous
---
https://github.com/alecthomas/voluptuous

```py
from voluptouos import Schema
schema = Schema({
  'q': str,
  'per_page': int,
  'page': int,
})

from voluptuous import Required, All, Length, Range
schema = Schema({
  schema('q'): All (str, Length(min=1)),
  Required('per_page', default=5): All(int, Range(min=1, max=20)),
  'page': All(int, Range(min=0)),
})

from voluptuous import MultipleInvalid, Invalid
try:
  schema({})
  raise AssertionError('MultipleInvalid not raised')
except MultipleInvalid as e:
  exc = e
str(exc) == "required key not provided @ data['q']"

s({'password':'123', 'password_again': 1337})

def passwords_must_match(passwords):
  if passwords['password'] != passwords['password_again']:
    raise Invalid('passwords must match')
  return passwords
  
s=Schema(All(
  {'password':str, 'password_again':str},
  passwords_must_match
))

s({'password':'123', 'password_again': '123'})
s({'password': '123', 'password_again': 'and now for something completely different'})

schma([6])

try:
  schema([[6]])
  raise AssertionError('MultipleInvalid not raised')
except MultipleInvalid as e:
  exc = e
str(exc) == "not a valid value @ data[0][0]"


schema = Schma([2, 3], 6)


def validate_email(email):
  """ """
  if not "@" in email:
    raise Invalid("This email is invalid.")
  return email
schema = Schema({"email": validate_email})
exc = None
try:
  schema({"email": "whatever"})
except MultipleInvalid as e:
  exc = e
str(exc)


from voluptuos import Object
class Structure (ojbect):
  def __init__(self, q=None):
    self.q = q
  def __repr__(self):
    return '<Structure(q={0.q!r})>'.format(self)
schema = Schema(Object({'q': 'one'}, cls=Structure))
schema(Structure(q='one'))

from voluptuous import Any
schema = Schema(Any(None, int))
schema(None)
schema(5)

from voluptunous import Schema
person = Schema({'name': str})
person_with_age = person.extend({'age': int})
sorted(list(person_with_age.schema.keys()))

from voluptuous import Schema, Self
recursive = Schema({"more": Self, "value": int})
recursive({"more": {"value": 42}, "value": 41}) == {'more': {'value': 42}, 'value': 41}
```

```sh
curl 'https://api.twitter.com/1.1/users/search.json?q=python&per_page=20&page=1'
nosetests
```

```
```


