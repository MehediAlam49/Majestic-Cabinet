# Majestic Cabinets

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=fff)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=fff)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![Responsive Design](https://img.shields.io/badge/design-responsive-2ea44f)](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Responsive_Design)
[![Font Awesome](https://img.shields.io/badge/icons-Font%20Awesome-528DD7?logo=fontawesome&logoColor=fff)](https://fontawesome.com/)
[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Majestic Cabinets is a responsive, multi-page brochure website for a Las Vegas cabinet company. It gives homeowners a clear way to explore cabinet services, review completed work, read renovation articles, and request a consultation or contact the business.

## Contents

- [Pages](#pages)
  - [Home](#home)
  - [About](#about)
  - [Services](#services)
  - [Portfolio](#portfolio)
  - [Articles](#articles)
  - [Article Details](#article-details)
  - [Contact](#contact)
- [Key Features](#key-features)
- [Tech Stack](#tech-stack)
- [Getting Started](#getting-started)
- [Environment Variables](#environment-variables)
- [Django Template Setup](#django-template-setup)
- [Context Data](#context-data)
- [Navigation Page](#navigation-page)
- [Usage](#usage)
- [License](#license)
- [Back to Contact](#back-to-contact)

## Pages

| Page            | File                                           | Purpose                                                                           |
| --------------- | ---------------------------------------------- | --------------------------------------------------------------------------------- |
| Home            | [`index.html`](index.html)                     | Introduces the company, services, portfolio, blog previews, and consultation CTA. |
| About           | [`about.html`](about.html)                     | Explains the company, team, experience, and business functions.                   |
| Services        | [`services.html`](services.html)               | Presents refinishing, refacing, and custom-built cabinet services.                |
| Portfolio       | [`portfolio.html`](portfolio.html)             | Displays the cabinet project gallery and category controls.                       |
| Articles        | [`articles.html`](articles.html)               | Lists cabinet-related articles and categories.                                    |
| Article Details | [`articlesDetails.html`](articlesDetails.html) | Shows the cabinet-refacing article detail view.                                   |
| Contact         | [`contact.html`](contact.html)                 | Provides the consultation form, business details, and map embed.                  |

## Key Features

- **Service discovery:** Highlights refinishing, refacing, custom cabinetry, design, and sales support.
- **Visual portfolio:** Uses project imagery from the `images/` directory to showcase completed cabinet work.
- **Editorial content:** Includes article listings, categories, and a detailed cabinet-refacing article.
- **Lead generation:** Provides consultation and email-subscription forms throughout the site.
- **Responsive presentation:** Uses shared CSS layouts designed for desktop and mobile viewports.
- **Business contact details:** Includes the Las Vegas address, phone numbers, email addresses, and an embedded Google Map.

## Tech Stack

- HTML5 for page structure and content
- CSS3 in [`style.css`](style.css) for layout, typography, responsive behavior, and visual styling
- WebP image assets in [`images/`](images/)
- Google Fonts: Open Sans, Oswald, Raleway, and Roboto
- Font Awesome 6.7.1 via CDN for interface icons
- Optional Django integration documented below; Django is not currently included in this repository

## Getting Started

### Prerequisites

- A modern web browser
- Optional: Python 3 for a local static HTTP server
- Optional: Git for cloning the repository

### Installation

Clone the repository and enter its directory:

```bash
git clone <repository-url>
cd Majestic-Cabinet
```

No package installation or build step is required for the current static implementation.

### Run locally

For the most reliable local behavior, serve the directory over HTTP:

```bash
python -m http.server 8000
```

Open [http://localhost:8000](http://localhost:8000) in a browser. You can also open [`index.html`](index.html) directly, although a local server is recommended for consistent asset and navigation behavior.

## Environment Variables

The current static site does not require environment variables. The forms and Google Map are front-end markup only; they do not currently submit data to a backend.

If the site is connected to a Django backend, a production deployment should keep secrets in environment variables, for example:

```env
DJANGO_SECRET_KEY=replace-with-a-secure-secret
DJANGO_DEBUG=False
DJANGO_ALLOWED_HOSTS=example.com,www.example.com
```

## Django Template Setup

The HTML files can be migrated into Django templates when server-side routing, reusable context, and form processing are needed. The following example assumes a Django project named `config` and an app named `website`.

### 1. Install and create the project

```bash
python -m venv .venv

# Windows PowerShell
.\.venv\Scripts\Activate.ps1

pip install django
django-admin startproject config .
python manage.py startapp website
python manage.py migrate
python manage.py runserver
```

### 2. Configure templates and static files

Move the HTML files to `website/templates/website/` and the CSS/images to `website/static/website/`. Add the app in `config/settings.py`:

```python
INSTALLED_APPS = [
	# ...
	"website",
]

STATIC_URL = "static/"
```

At the top of each converted template, load static assets:

```django
{% load static %}
<link rel="stylesheet" href="{% static 'website/style.css' %}">
<img src="{% static 'website/images/logo.webp' %}" alt="Majestic Cabinets logo">
```

### 3. Add a template view

Create `website/views.py`:

```python
from django.shortcuts import render


def home(request):
	context = {
		"page_title": "Majestic Cabinets",
		"featured_services": [
			"Refinishing",
			"Refacing",
			"Custom Built",
		],
	}
	return render(request, "website/index.html", context)
```

### 4. Add named URL patterns

Create `website/urls.py`:

```python
from django.urls import path

from . import views

app_name = "website"

urlpatterns = [
	path("", views.home, name="home"),
]
```

Include the app URLs in `config/urls.py`:

```python
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
	path("admin/", admin.site.urls),
	path("", include("website.urls")),
]
```

## Context Data

Pass page content from views instead of hard-coding repeated values in every template:

```python
def services(request):
	context = {
		"page_title": "Services",
		"services": [
			{
				"name": "Refinishing",
				"image": "website/images/ourServices1.webp",
				"summary": "Refresh existing cabinets without replacing the full kitchen.",
			},
			{
				"name": "Refacing",
				"image": "website/images/ourServices2.webp",
				"summary": "Update doors, drawer fronts, and hardware while keeping the layout.",
			},
			{
				"name": "Custom Built",
				"image": "website/images/ourServices3.webp",
				"summary": "Create cabinetry designed around the room and the homeowner's needs.",
			},
		],
	}
	return render(request, "website/services.html", context)
```

Render the context in `website/templates/website/services.html`:

```django
{% extends "website/base.html" %}
{% load static %}

{% block content %}
<h1>{{ page_title }}</h1>
<div class="services-grid">
  {% for service in services %}
	<article>
	  <img src="{% static service.image %}" alt="{{ service.name }}">
	  <h2>{{ service.name }}</h2>
	  <p>{{ service.summary }}</p>
	</article>
  {% empty %}
	<p>No services are available.</p>
  {% endfor %}
</div>
{% endblock %}
```

## Navigation Page

Use Django URL names instead of hard-coded `.html` paths. This keeps navigation working when URL patterns change:

```django
<nav aria-label="Primary navigation">
  <a href="{% url 'website:home' %}">Home</a>
  <a href="{% url 'website:about' %}">About</a>
  <a href="{% url 'website:services' %}">Services</a>
  <a href="{% url 'website:portfolio' %}">Portfolio</a>
  <a href="{% url 'website:articles' %}">Articles</a>
  <a href="{% url 'website:contact' %}">Contact</a>
</nav>
```

The matching named routes can be defined as follows:

```python
urlpatterns = [
	path("", views.home, name="home"),
	path("about/", views.about, name="about"),
	path("services/", views.services, name="services"),
	path("portfolio/", views.portfolio, name="portfolio"),
	path("articles/", views.articles, name="articles"),
	path("articles/<slug:slug>/", views.article_detail, name="article-detail"),
	path("contact/", views.contact, name="contact"),
]
```

## Usage

### Browse the static site

```text
Home:           /index.html
About:          /about.html
Services:       /services.html
Portfolio:      /portfolio.html
Articles:       /articles.html
Article detail: /articlesDetails.html
Contact:        /contact.html
```

Use the primary pages to review services and project images. Use the Contact page to view business information, the map, and the consultation form. In the current static version, form submission is not connected to email or database storage.

### Contact link

Use this link from any static page to return visitors to the contact page:

```html
<a href="contact.html">Request a consultation</a>
```

For the Django version, use the named route:

```django
<a href="{% url 'website:contact' %}">Request a consultation</a>
```

## License

This project is released under the [MIT License](https://opensource.org/licenses/MIT). Add a `LICENSE` file containing the standard MIT License text before distributing the project in production.

## Back to Contact

[Return to the Contact page](contact.html) to view the consultation form, address, phone numbers, and map.
