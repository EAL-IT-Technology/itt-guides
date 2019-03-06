---
layout: guide
date:   2019-03-05 12:00:00 +0200
title:  Using REST APIs
categories: tech
status: beta
---

# Background

REST APIs is a way to expose data to users using HTTP(S). It is (always?) a stateless service, that returns machine readable data e.g. in [XML](https://da.wikipedia.org/wiki/XML) or [JSON](https://www.json.org/) format.

It is often used in conjunction with javascript to make more dynamic pages.

References for RESTfull APIs:

* [Understanding And Using REST APIs](https://www.smashingmagazine.com/2018/01/understanding-using-rest-api/)
* [Learn REST: A RESTful Tutorial](https://www.restapitutorial.com/)

We will use [gitlab.com](https://docs.gitlab.com/ee/api/) API as an example. It is fairly understandable, when you know the web interface.

# Using curl - read only

Note: adding `-v` to curl will show the HTTP communication, not just the result.

Fetch list of [user projects](https://docs.gitlab.com/ee/api/projects.html#list-user-projects)

```
$ curl https://gitlab.com/api/v4/users/moozer/projects
[{"id":10744714,"description":"","name":"kvm-speedtest","name_with_namespace":"Moozer / kvm-speedtest","path":"kvm-speedtest","path_with_namespace":"moozer/kvm-speedtest","created_at":"2019-02-07T23:28:02.389Z","default_branch":"master","tag_list":[],"ssh_url_to_repo":"git@gitlab.com:moozer/kvm-speedtest.git","http_url_to_repo":"https://gitlab.com/moozer/kvm-speedtest.git","web_url":"https://gitlab.com/moozer/kvm-speedtest","readme_url":"https://gitlab.com/moozer/kvm-speedtest/blob/master/readme.md","avatar_url":null,"star_count":0,"forks_count":0,"last_activity_at":"2019-02-18T13:22:50.613Z","namespace":{"id":1441266,"name":"moozer","path":"moozer","kind":"user","full_path":"moozer","parent_id":null}},
...,{"id":9268585,"description":"","name":"minimal-ci","name_with_namespace":"Moozer / minimal-ci","path":"minimal-ci","path_with_namespace":"moozer/minimal-ci","created_at":"2018-11-07T22:17:50.901Z","default_branch":"master","tag_list":[],"ssh_url_to_repo":"git@gitlab.com:moozer/minimal-ci.git","http_url_to_repo":"https://gitlab.com/moozer/minimal-ci.git","web_url":"https://gitlab.com/moozer/minimal-ci","readme_url":null,"avatar_url":null,"star_count":0,"forks_count":0,"last_activity_at":"2018-11-26T12:17:33.914Z","namespace":{"id":1441266,"name":"moozer","path":"moozer","kind":"user","full_path":"moozer","parent_id":null}}]
```

The API includes all kinds of requests to everything (?) that is available on the website also. I usually fetch files and issues.

### Pagination

A given request will not return thousands of records - default for gitlab is 20 for issues. You can request other "pages" than the first.

Fetch list of projects, limit to 2 entries per page and show page 2.
```
$ curl https://gitlab.com/api/v4/users/moozer/projects\?per_page\=2\&page\=2
```

# Using curl - authenticated

In order to do stuff and see private information you need to be authorized. This is done using [personal access tokens](https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html)

Note that I use `jq` to make the output shorter and more to the point. The program homepage is [here](https://stedolan.github.io/jq/).

The one used in the example is `JCvGpfoqLBT5or7qKSBy` (and is deleted before this guide is published).

Without authentication
```
$ curl -s 'https://gitlab.com/api/v4/users/1207689/projects' | jq '.[].name'
"kvm-speedtest"
"document_templates"
"docker-pdf"
"GitLab Community Edition"
"exsi-tools"
"ansible-server-radicale"
"minimal-ci"
```

With authentication, the list is longer including private repos.
```
$  curl -s 'https://gitlab.com/api/v4/users/1207689/projects?private_token=JCvGpfoqLBT5or7qKSBy' | jq '.[].name'
"kvm-speedtest"
"19S-ITT2-project"
"document_templates"
"gitlab-runner-test"
"docker-pdf"
"pdf-ci"
"GitLab Community Edition"
"ex-python-network"
"exsi-tools"
"minimal-ci-packer"
"ansible-server-radicale"
"minimal-ci"
"ProjectNetworkWeek48-49"
```


# Using python

Whenever you want to work with REST APIs and python, start by checking if someone has already made a module for you to use. In this case there is a complete one called [gitlab](https://python-gitlab.readthedocs.io/en/stable/).

Go [here](https://gitlab.com/EAL-ITT/19s-itt2-project/blob/master/scripts/gitlab/fetch_groups.py) for an example
