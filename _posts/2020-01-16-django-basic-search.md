---
title: Very Basic Search Component With Django
layout: post
---

I didn't write Django for a long time but I took an offer from a good company at the same time my closest friends write their thesis because of those reasons I looked to Django again.

My friends need to make a search bar for a really small set of data. First I made a new page for search and in this page there is a search bar. You write your word and you need to click to search button. Yes, that was an easy way but after that I back to my home and I thought that If I can make an endpoint and Ajax call to that endpoint this can be much better user experience and can be used for template.

That was the first version of the code:
```python
# ~/views.py

from django.http import JsonResponse

def ajax_search(request):
    if(request.method == "POST"):
        lectureQueryset = ""
        word = request.POST["word"]
        if word is not None:
            lectureQueryset = Lecture.objects.all()
            lectureQueryset = lectureQueryset.filter(name__icontains=word)
            lecturesArray = []
            for lecture in lectureQueryset:
                lectureObject = {}
                lectureObject["name"] = lecture.name
                lectureObject["pk"] = lecture.pk
                lecturesArray.append(lectureObject)
        return JsonResponse({"lectures": lecturesArray},status=200)
```
That was the example code because of that I only returned 200. The most important thing is in this code is searching method which is ```name__icontains```.

```html
<!-- ~/search-bar.html -->

<form action={ % url 'ajax_search' %} id="ajax-search-form" method="POST" class="post-form">
    { % csrf_token %}
    <input name="search-value" id="ajax-search-value" style="width: 100%">
</form>
<div id="ajax-search-result-container" style="overflow-y: auto; max-height: 90px; margin-top: 10px;">
</div>
```

I made an form only with input for synchronous searching and I made container for showing results. 

```javascript
// ~/searchBarJavaScript.js

/*
 *
 *  Taking CSRF token for authorization
 *
 */
// CSRF Token Usage on Ajax from https://stackoverflow.com/questions/19333098403-forbidden-error-when-making-an-ajax-post-request-in-django-framework
// Getting token starts

function getCookie(name) {
    var cookieValue = null;
    if (document.cookie && document.cookie != '') {
        var cookies = document.cookie.split(';');
        for (var i = 0; i < cookies.length; i++) {
            var cookie = jQuery.trim(cookies[i]);
            // Does this cookie string begin with the name we want?
            if (cookie.substring(0, name.length + 1) == (name + '=')) {
                cookieValue = decodeURIComponent(cookie.substring(name.length + 1));
                break;
            }
        }
    }
    return cookieValue;
}
var csrftoken = getCookie('csrftoken');

//Ajax call
function csrfSafeMethod(method) {
    // these HTTP methods do not require CSRF protection
    return (/^(GET|HEAD|OPTIONS|TRACE)$/.test(method));
}
// Getting token end

const searchForm = document.getElementById('ajax-search-form');
const searchButton = document.getElementById('ajax-search-button');
const url = searchForm.action;

const createAnchorsArray = (lectures) => {
    const anchors = [];
    for (lecture of lectures) {
        const anchor = document.createElement("a");
        anchor.href = `lecture/${lecture["pk"]}`
        anchor.innerHTML = `${lecture["name"]}`
        anchors.push(anchor)
    }

    return anchors;
}

const appendSearchResults = (anchors) => {
    const resultsContainer = document.getElementById("ajax-search-result-container");
    resultsContainer.innerHTML += "<br>"
    for (const anchor of anchors) {
        resultsContainer.append(anchor);
        resultsContainer.innerHTML += "<hr>"
    }
}

const submitFormFunction = () => {
    document.getElementById("ajax-search-result-container").innerHTML = "";

    $.ajaxSetup({
        crossDomain: false, // obviates need for sameOrigin test
        beforeSend: function(xhr, settings) {
            if (!csrfSafeMethod(settings.type)) {
                xhr.setRequestHeader("X-CSRFToken", csrftoken);
            }
        }
    });

    $.ajax({
        type: 'POST',
        url: url,
        data: {
            word: document.querySelector('#ajax-search-form #ajax-search-value').value
        },
        success: function(response) {
            const anchorsArray = createAnchorsArray(response["lectures"]);
            appendSearchResults(anchorsArray);
        },
        error: function(response) {
            console.warn(response.statusText);
        }
    })
}

searchForm.addEventListener("submit", function(event){
        event.preventDefault();
        submitFormFunction();
    }
)

document.querySelector('#ajax-search-form #ajax-search-value').addEventListener("keypress", function(event){
        submitFormFunction()
    }
)
```

I'm a lazy person because of that I took the generic taking csrf from stackoverflow.


```python
# ~/urls.py

from django.conf.urls import url

urlpatterns = [
    # ...
	url('^ajax_search/$', views.ajax_search, name = "ajax_search"),
]
```