---
description: 프로젝트 관련 API 정의 문서
---

# Projects

## Create a new project

{% swagger method="post" path="/projects/" baseUrl="http://loaclhost:8000/api/v1" summary="" %}
{% swagger-description %}
To create a new project
{% endswagger-description %}

{% swagger-parameter in="body" name="projectTitle" type="string" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="projectDescription" type="string" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="githubLink" type="string " required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="demositeLink" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="previewImages" type="file[]" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="projectHashtag" type="string[]" required="false" %}

{% endswagger-parameter %}

{% swagger-response status="201: Created" description="" %}
```javascript
{
    "id": "f31473c9-2362-4ddd-8b83-6283f35f54ef",
    "previewImages": [
        "https://whatprojectyouwant.s3.amazonaws.com/project_image/%7Bproject.id%7D/prp.gif",
        "https://whatprojectyouwant.s3.amazonaws.com/project_image/%7Bproject.id%7D/default_profile.png"
    ],
    "projectHashtag": [
        "project",
        "flask",
        "react",
        "docker"
    ],
    "projectTitle": "PRP(for your portrait right protection)",
    "projectDescription": "업로드 할 당신의 영상 속 인물들의 초상권을 보호할 수 있도록 이 서비스를 이용해보세요",
    "githubLink": "https://github.com/PRP-for-your-portrait-right-protection",
    "demositeLink": "https://github.com/PRP-for-your-portrait-right-protection",
    "views": 0,
    "likes": 0,
    "created": "2023-02-14T05:39:39.958595Z"
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}



## Get a project list&#x20;

{% swagger method="get" path="projects/" baseUrl="http://loacalhost:8000/api/v1/" summary="Project" %}
{% swagger-description %}
It receives 20 data at once

API URL  Example:&#x20;

http://localhost:8000/api/v1/projects/?ordering=views\&search=js\&page=1



You need '-'  to show reverse order for most recent data

http://localhost:8000/api/v1/projects/?ordering=-likes

http://localhost:8000/api/v1/projects/?ordering=-views



If 'ordering' is omitted it is same as 'ordering= -created' to show most recet data&#x20;




{% endswagger-description %}

{% swagger-parameter in="query" name="ordering" type="string" %}
There are 3 types: created, views, likes
{% endswagger-parameter %}

{% swagger-parameter in="query" name="search" type="string" %}
search keywords by project title
{% endswagger-parameter %}

{% swagger-parameter in="query" name="page" type="Int" required="false" %}
pagination page
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "count": 87,//number of current data
    "next": "http://127.0.0.1:8000/projects/?page=2",//next page url
    "previous": null,//previous page url 
    "results": [
        {
            "id": "f31473c9-2362-4ddd-8b83-6283f35f54ef",
            "previewImages": [
                "https://whatprojectyouwant.s3.amazonaws.com/project_image/%7Bproject.id%7D/prp.gif",
                "https://whatprojectyouwant.s3.amazonaws.com/project_image/%7Bproject.id%7D/default_profile.png"
            ],
            "projectHashtag": [
                "project",
                "flask",
                "react",
                "docker"
            ],
            "projectTitle": "PRP(for your portrait right protection)",
            "projectDescription": "업로드 할 당신의 영상 속 인물들의 초상권을 보호할 수 있도록 이 서비스를 이용해보세요",
            "githubLink": "https://github.com/PRP-for-your-portrait-right-protection",
            "demositeLink": "https://github.com/PRP-for-your-portrait-right-protection",
            "views": 0,
            "likes": 0,
            "created": "2023-02-14"
        },
        ...
    ]
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="401" description="" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

## Get a project detail&#x20;

{% swagger method="get" path="projects/<:projectId>/" baseUrl="http://loaclhost:8000/api/v1/" summary="if you use this API it updates view counts  " %}
{% swagger-description %}
API URL  Example:&#x20;

http://localhost:8000/api/v1/projects/550e8400-e29b-41d4-a716-446655440000/


{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="string" required="true" %}
project ID (UUID)
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
//Need to add comment section . 
    "id": "f31473c9-2362-4ddd-8b83-6283f35f54ef",
    "previewImages": [
        "https://whatprojectyouwant.s3.amazonaws.com/project_image/%7Bproject.id%7D/prp.gif",
        "https://whatprojectyouwant.s3.amazonaws.com/project_image/%7Bproject.id%7D/default_profile.png"
    ],
     "comment": [
        {
            "id": "c2265d31-9d52-44e2-afd4-4beb933626f5",
            "content": "I love this project!",
            "created": "2023-02-14T09:55:39.503102Z",
            "status": 1,
            "activate_date": "2023-02-14T09:55:39.502862Z",
            "deactivate_date": null
        },
        {
            "id": "6fda5e13-0cde-4772-bb33-3f126ceb48c0",
            "content": "Good job!",
            "created": "2023-02-14T09:55:37.319294Z",
            "status": 1,
            "activate_date": "2023-02-14T09:55:37.318894Z",
            "deactivate_date": null
        },
        {
            "id": "2e7db03b-acf4-4a19-8423-fe1651b773d6",
            "content": "Nice work!",
            "created": "2023-02-14T09:54:36.939222Z",
            "status": 1,
            "activate_date": "2023-02-14T09:54:36.938863Z",
            "deactivate_date": null
        }
    ],
    "projectHashtag": [
        "project",
        "flask",
        "react",
        "docker"
    ],
    "projectTitle": "PRP(for your portrait right protection)",
    "projectDescription": "업로드 할 당신의 영상 속 인물들의 초상권을 보호할 수 있도록 이 서비스를 이용해보세요",
    "githubLink": "https://github.com/PRP-for-your-portrait-right-protection",
    "demositeLink": "https://github.com/PRP-for-your-portrait-right-protection",
    "views": 0,
    "likes": 0,
    "created": "2023-02-14T05:39:39.958595Z"
}
```
{% endswagger-response %}
{% endswagger %}

## Increase project like

{% swagger method="patch" path="projects/<:projectId>/likes/" baseUrl="http://loaclhost:8000/api/v1/" summary="" %}
{% swagger-description %}
Use this API to increase project like 
{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="string" required="true" %}
project ID (UUID)
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "id": "f31473c9-2362-4ddd-8b83-6283f35f54ef",
    "previewImages": [
        "https://whatprojectyouwant.s3.amazonaws.com/project_image/%7Bproject.id%7D/prp.gif",
        "https://whatprojectyouwant.s3.amazonaws.com/project_image/%7Bproject.id%7D/default_profile.png"
    ],
    "projectHashtag": [
        "project",
        "flask",
        "react",
        "docker"
    ],
    "projectTitle": "PRP(for your portrait right protection)",
    "projectDescription": "업로드 할 당신의 영상 속 인물들의 초상권을 보호할 수 있도록 이 서비스를 이용해보세요",
    "githubLink": "https://github.com/PRP-for-your-portrait-right-protection",
    "demositeLink": "https://github.com/PRP-for-your-portrait-right-protection",
    "views": 0,
    "likes": 1,//likes have increased. 
    "created": "2023-02-14T05:39:39.958595Z"
}
```
{% endswagger-response %}
{% endswagger %}

## Create Comment

{% swagger method="post" path="projects/<:projectId>/comments/" baseUrl="http://loaclhost:8000/api/v1/" summary="" %}
{% swagger-description %}
To create comment in specific project&#x20;

It generates  anonymous username
{% endswagger-description %}

{% swagger-parameter in="body" name="content" type="string" required="true" %}
comment content
{% endswagger-parameter %}

{% swagger-response status="201: Created" description="" %}
```javascript
{
    "id": "b2b7948c-0044-4f3c-87ed-69303f803e0e",
    "nickname": "지루한 혁명가",
    "content": "저도 써보고 싶어요!",
    "created": "2023-02-19"
}
```
{% endswagger-response %}
{% endswagger %}



