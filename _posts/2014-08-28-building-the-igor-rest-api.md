---
layout: post
title: Building the Igor REST API
tags: gsoc2014
---

This weekend marks the end of my GSoC with OSUOSL. We now have a full-fledged
[REST API][1], a [hierarchical CLI][2] and more than a couple of
[patches to pyipmi][3] implementing IPMI commands. I have already
[talked about][4] the CLI before the midterm evaluation. In this post,
I will focus on the Igor REST API that the CLI delegates all the heavy lifting
to.

## Design

The decision to split the overall project into two pieces (the REST API and the
CLI) was motivated by the need of having multiple possible clients: Android
applications, web applications and curses interfaces, to name a few. Having this
server-client dichotomy helps us write the core logic, error handling and tests
once for the server, and have our clients be really thin. This is also the
philosophy embodied by the [Heroku CLI][5].

The REST API serves a dual purpose: to manage machines, users and regulate their
interactions, and to call the actual IPMI commands. The following diagram
depicts a bird's-eye view of the architecture:

![Igor Architecture](https://docs.google.com/drawings/d/1KZ2L9Hj7nB1S1TfYvx17_ZtXdjvPtdZdmY92QE4KKlI/pub?w=960&amp;h=720 "Igor Architecture")

*[Diagram source](https://docs.google.com/drawings/d/1KZ2L9Hj7nB1S1TfYvx17_ZtXdjvPtdZdmY92QE4KKlI/edit?usp=sharing)*

Machines and users are standard resources in this architecture, accessible via
endpoints that accept the GET, PUT, POST and DELETE verbs. In the
back-end, both machines and users are represented by their own database
[models][6].

The API regulates interactions between the two via *permissions*: a many-to-many
relationship between users and machines. An IPMI command can be initiated by a
user targeting a machine only if such a permission exists between the user and
that machine. Permissions can be granted and revoked via PUT and DELETE requests
to the permissions endpoint.

The API is implemented as a Flask application using [flask-restful][7].
flask-restful wraps Flask's method-based dispatching and [pluggable views][8],
providing convenient abstractions for REST applications.

## Users, Machines, Authentication and Authorization

Access regulations are of two kinds: authentication and authorization.
Authentication performs endpoint-wide blocking and ensures the user has valid
credentials. Authorization checks if users are permitted to access the specific
machine they are attempting management or IPMI operations on.

Both [authentication][9] and [authorization][10] are implemented as decorators.
Protecting an endpoint then simply involves decorating the flask-restful resource
class for that endpoint. The only tricky bit is the order of applied decorators:
we want authentication to take place before authorization, and must hence place
authorization *before* authentication in the decorators array
(decorators are applied outward-in).

Separate modules each implement the [user management endpoints][11],
[machine management endpoints][12] and [permissions endpoints][13]. The
[routes module][14] collects these and the IPMI operation endpoints into a list
and registers them with the application. Having this module separate helps us
look at a map of all the available endpoints. The endpoint list also helps us
in testing, as we will see in an upcoming section.

## IPMI Operations

IPMI operations are implemented via my [fork of pyipmi][15]. pyipmi wraps calls
to [ipmitool][16] and [freeipmi][17], parses their response and returns them as
Python data structures.

Each command is called within the methods of a resource, which is a subclass of
`IPMIResource`. `IPMIResource` obtains the target hostname that is set by the
authorization decorator and creates the necessary pyipmi objects to access that
machine. Each command is called via a [wrapper][18] that makes the call,
obtains the response and returns a HTTP 400 (bad request) if the command fails,
otherwise passes through to the rest of the method body. Since most
error-handling is delegated to ipmitool, the calls are thin and easily
adaptable in case the underlying command changes. All the IPMI operation
endpoints are implemented in a [single module][19].

Unfortunately, the company maintaining pyipmi [shut down][20] and the project
is now unmaintained. Nevertheless, it appears to be the most full-fledged
Python-IPMI interface available right now. The IPMI `lan alert` [command][21],
`sel delete` [command][22] and [sensor][23] commands were contributed back to
pyipmi during the course of this work.

## Tests

Tests were implemented with [nose][24] as the test collector/runner,
and [flask-testing][25] providing a nice abstraction over Python's
built-in `unittest` module that makes it convenient to test Flask applications.
A [pull request][26] contributing optional test-failure messages was merged into
flask-testing during the course of this work.

Each test is set up by creating a new database instance with a single root user.
The current bunch of tests consists of four modules: authentication tests, user
management tests, machine management tests and permission tests.

The [authorization tests][27] take advantage of the resources list in the routes
module described earlier. Each endpoint (except the root at /) is verified to be
inaccessible without authentication. The [user][28] and [machine][29] management
tests verify CRUD operations on the respective endpoints, in addition to
additional cases such as adding users/machines that already exist. The
[permission tests][30] verify the addition and removal of users-machines
relationships via the API endpoints.

## Future

The most important extension to this work is closely tied to the development of
one of the following pure Python implementations of the IPMI protocol:
[xcat python-ipmi][31], [kontron python-ipmi][32] or [pyghmi][33]. Once these
libraries reasonably cover the complete IPMI protocol, they can be integrated
into the Igor REST API. Both the API and CLI architecture would remain the same
with this change.

This can be followed by a good implementation of serial-on-LAN (SOL), which was
[planned][34] for this project but abandoned due to poor fit with the REST
protocol, since implementing SOL over REST would require maintaining server-side
state for each user. The SOL is asynchronous and full-duplex by nature, and
per-user queues could (not very elegantly) replicate this functionality over
REST. The proposed architecture was as depicted below:

![Igor SOL Design](https://docs.google.com/drawings/d/1YiY9cBmCVGKoQG-12gxCHKqPBhJaLBg977aIyM7tgYs/pub?w=804&h=627 "Igor SOL Design")

*[Diagram source](https://docs.google.com/drawings/d/1YiY9cBmCVGKoQG-12gxCHKqPBhJaLBg977aIyM7tgYs/edit?usp=sharing)*

This may be better thought about after having the pure Python IPMI protocol
implementation.

Further extensions are the tasks I could not complete due to the unplanned work
on patching pyipmi: the ncurses TUI, the Flask web GUI and the Android
application. These client interfaces would further improve the IPMI
accessibility of OSL machines, and also test the robustness of the REST API.

[1]: https://github.com/emaadmanzoor/igor-rest-api
[2]: https://github.com/emaadmanzoor/igor-cli
[3]: https://github.com/emaadmanzoor/pyipmi/pulls?q=is%3Apr+is%3Aclosed
[4]: http://eyeshalfclosed.com/blog/2014/06/26/building-the-igor-cli-with-click/
[5]: https://devcenter.heroku.com/articles/heroku-command
[6]: https://github.com/emaadmanzoor/igor-rest-api/blob/master/api/models.py
[7]: http://flask-restful.readthedocs.org/en/latest/
[8]: http://flask.pocoo.org/docs/views/#method-based-dispatching
[9]: https://github.com/emaadmanzoor/igor-rest-api/blob/master/api/login.py#L12-L21
[10]: https://github.com/emaadmanzoor/igor-rest-api/blob/master/api/login.py#L23-L41
[11]: https://github.com/emaadmanzoor/igor-rest-api/blob/master/api/users.py
[12]: https://github.com/emaadmanzoor/igor-rest-api/blob/master/api/machines.py
[13]: https://github.com/emaadmanzoor/igor-rest-api/blob/master/api/permissions.py
[14]: https://github.com/emaadmanzoor/igor-rest-api/blob/master/api/routes.py
[15]: https://github.com/emaadmanzoor/pyipmi/
[16]: http://sourceforge.net/projects/ipmitool/
[17]: http://www.gnu.org/software/freeipmi/
[18]: https://github.com/emaadmanzoor/igor-rest-api/blob/master/api/utils.py#L7-L12
[19]: https://github.com/emaadmanzoor/igor-rest-api/blob/master/api/ipmi.py
[20]: http://arstechnica.com/information-technology/2013/12/arm-in-the-server-room-faces-a-set-back-as-calxeda-shuts-down/
[21]: https://github.com/emaadmanzoor/pyipmi/pull/1
[22]: https://github.com/emaadmanzoor/pyipmi/pull/2
[23]: https://github.com/emaadmanzoor/pyipmi/pull/3
[24]: https://nose.readthedocs.org/en/latest/
[25]: http://flask.pocoo.org/docs/testing/
[26]: https://github.com/jarus/flask-testing/pull/59
[27]: https://github.com/emaadmanzoor/igor-rest-api/blob/master/tests/login_tests.py
[28]: https://github.com/emaadmanzoor/igor-rest-api/blob/master/tests/users_tests.py
[29]: https://github.com/emaadmanzoor/igor-rest-api/blob/master/tests/machine_tests.py
[30]: https://github.com/emaadmanzoor/igor-rest-api/blob/master/tests/permission_tests.py
[31]: https://github.com/xcat-org/python-ipmi
[32]: https://github.com/kontron/python-ipmi
[33]: https://github.com/stackforge/pyghmi
[34]: https://github.com/emaadmanzoor/igor-rest-api/blob/master/docs/SOL.md
