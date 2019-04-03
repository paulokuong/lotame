[![Build Status](https://travis-ci.org/paulokuong/lotame.svg?branch=master)](https://travis-ci.org/paulokuong/lotame)[![Coverage Status](https://coveralls.io/repos/github/paulokuong/lotame/badge.svg?branch=master)](https://coveralls.io/github/paulokuong/lotame?branch=master)
Lotame API Wrapper
==================

Requirements
------------

* Python 3.6 (tested)

Installation
------------
```
    pip install lotame
```

Goal
----

To provide a generic wrapper Lotame API

Code sample
-----------


```python
    from lotame.lotame import Lotame
    l = Lotame(username='xxxx', password='yyyy')
```
or setting the following environment variables:
```
LOTAME_USERNAME
LOTAME_PASSWORD
```
then simply
```
    from lotame.lotame import Lotame
    l = Lotame()
```

Search audiences
```python
    audiences = l.get('audiences/search', searchTerm='Age - ').json()['Audience']
```
Get behavior 3333
```python
    behavior = l.get('behaviors/{}'.format(3333)).json()
```
Create audience segment with 3 behaviors.
```python
    audience_definition = l.get_create_audience_json(
        'Lotame api test 5',
        2215, [[6322283, 6322292], [6322283, 6322292]],
        'Testing out Lotame API 5')
    post_response_json = l.post('audiences', audience_definition).json()
    print(post_response_json)
```
Create audience segment with 3 behaviors for (My Profile)
```python
    audience_definition = l.get_create_audience_json(
        'Lotame api test 5',
        2215, [[6322283, 6322292, 1111760, 6322303], [6322283, 6322292, 1111760, 6322303]],
        'Testing out Lotame API 5', overlap=True)
```
Create audience segment with 3 behaviors for (All Profile)
```python
    audience_definition = l.get_create_audience_json(
        'Lotame api test 5',
        2215, [[6322283, 6322292, 1111760, 6322303], [6322283, 6322292, 1111760, 6322303]],
        'Testing out Lotame API 5', overlap=False)
```
Getting Reach Estimate (Note that description param is removed since it is not valid param)
```python
    audience_definition = l.get_create_audience_json(
        'Lotame api test 8',
        2215, [[6322283, 6322292, 1111760, 6322303], [6322283, 6322292, 1111760, 6322303]])
    reach_estimates = l.post('audiences/reachEstimates', audience_definition).json()
    reach_estimates_res = l.get('audiences/reachEstimates/{}'.format(reach_estimates.get('id')))
    print(reach_estimates_res.json())
```
Getting behaviors under hierarchy tree at depth 2 child nodes.
```python
    [{'name':j['name'],'behavior_id':j['behaviorId']}
    for j in l.get('hierarchies/525000', depth=2).json().get('nodes')[1].get('childNodes')]
```

Getting report for audience profile
```python
    res = l.get('reports/audiences/{audience_id}/profile/type/{audience_profile_report_type_id}'.format(
        audience_id=333333,audience_profile_report_type_id=6))
```

Contributors
------------

* Paulo Kuong ([@pkuong](https://github.com/paulokuong))
