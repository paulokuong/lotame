| |Build Status|

Lotame API Wrapper
------------------

Wrapper Class for Lotame API.

    | Fully unit tested wrapper class for Lotame REST API.
    | https://api.lotame.com/docs
    | https://github.com/paulokuong/lotame

Requirements
------------

-  Python 3.6 (tested)

Goal
----

| To provide a generic wrapper Lotame API

Code sample
-----------

| Instantiate

.. code:: python

    from lotame.lotame import Lotame
    l = Lotame(username='xxxx', password='yyyy')

| Search audiences

.. code:: python

    audiences = l.get('audiences/search', searchTerm='Age - ').json()['Audience']

| Get behavior 3333

.. code:: python

    behavior = l.get('behaviors/{}'.format(3333)).json()

| Create audience segment with 3 behaviors.

.. code:: python

    audience_definition = l.get_create_audience_json(
        'Lotame api test 5',
        2215, [[6322283, 6322292], [6322283, 6322292]],
        'Testing out Lotame API 5')
    post_response_json = l.post('audiences', audience_definition).json()
    print(post_response_json)

| Create audience segment with 3 behaviors for (My Profile)

.. code:: python

    audience_definition = l.get_create_audience_json(
        'Lotame api test 5',
        2215, [[6322283, 6322292, 1111760, 6322303], [6322283, 6322292, 1111760, 6322303]],
        'Testing out Lotame API 5', overlap=True)

| Getting Reach Estimate (Note that description param is removed since it is not valid param)

.. code:: python

    audience_definition = l.get_create_audience_json(
        'Lotame api test 8',
        2215, [[6322283, 6322292, 1111760, 6322303], [6322283, 6322292, 1111760, 6322303]])
    reach_estimates = l.post('audiences/reachEstimates', audience_definition).json()
    reach_estimates_res = l.get('audiences/reachEstimates/{}'.format(reach_estimates.get('id')))
    print(reach_estimates_res.json())

| Getting behaviors under hierarchy tree at depth 2 child nodes.

.. code:: python

    [{'name':j['name'],'behavior_id':j['behaviorId']}
    for j in l.get('hierarchies/525000', depth=2).json().get('nodes')[1].get('childNodes')]

| Getting report for audience profile

.. code:: python

    res = l.get('reports/audiences/{audience_id}/profile/type/{audience_profile_report_type_id}'.format(
        audience_id=333333,audience_profile_report_type_id=6))

Contributors
------------

-  Paulo Kuong (`@pkuong`_)

.. _@pkuong: https://github.com/paulokuong

.. |Build Status| image:: https://travis-ci.org/paulokuong/lotame.svg?branch=master
.. target: https://travis-ci.org/paulokuong/lotame
