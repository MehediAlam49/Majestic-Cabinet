# Majestic Cabinets

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=fff)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=fff)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![Responsive Design](https://img.shields.io/badge/design-responsive-2ea44f)](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Responsive_Design)
[![Font Awesome](https://img.shields.io/badge/icons-Font%20Awesome-528DD7?logo=fontawesome&logoColor=fff)](https://fontawesome.com/)
[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Contents

- [Pages](#pages)
  - [Home](#home)
  - [About](#about)
  - [Services](#services)
  - [Portfolio](#portfolio)
  - [Articles](#articles)
  - [Article Details](#article-details)
  - [Contact](#contact)
- [Shared Stylesheet and Assets](#shared-stylesheet-and-assets)
- [Key Features](#key-features)
- [Tech Stack](#tech-stack)
- [Tools Setup](#tools-setup)
  - [Code Editor](#code-editor)
  - [Git](#git)
  - [Browser and Developer Tools](#browser-and-developer-tools)
  - [Python Static Server](#python-static-server)
  - [External Font and Icon Tools](#external-font-and-icon-tools)
  - [Image Asset Workflow](#image-asset-workflow)
  - [Optional Django Tools](#optional-django-tools)
- [Getting Started](#getting-started)
- [Environment Variables](#environment-variables)
- [Django Template Setup](#django-template-setup)
- [Context Data](#context-data)
- [Navigation Page](#navigation-page)
- [Usage](#usage)
- [License](#license)
- [Back to Contact](#back-to-contact)

Majestic Cabinets is a responsive, multi-page brochure website for a Las Vegas cabinet company. It gives homeowners a clear way to explore cabinet services, review completed work, read renovation articles, and request a consultation or contact the business.

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

### Home

[`index.html`](index.html) is the primary landing page. It combines the main promotion, company introduction, service highlights, portfolio preview, reasons to choose the company, recent article previews, email subscription form, and footer contact details.

```html
<h1>
  Refinish Your Cabinets <br />
  Save Up To 60%
</h1>
<p>Call us today for your FREE design consultation</p>
<a href="contact.html">Request a quote</a>
```

### About

[`about.html`](about.html) explains the company history, quality promise, design and innovation functions, team members, and contractor licensing information. It is intended for visitors who need more trust and company background before requesting a quote.

```html
<h1>About us</h1>
<p>HOME / ABOUT</p>
<h2>Welcome to <span>Majestic Cabinets</span></h2>
```

### Services

[`services.html`](services.html) presents the three core cabinet services: refinishing, refacing, and custom-built cabinetry. Each service uses an image from `images/` and a descriptive paragraph so visitors can compare the available options.

```html
<article class="service">
  <img src="images/ourServices1.webp" alt="Cabinet refinishing" />
  <h4>Refinishing</h4>
  <p>Refresh existing cabinets without replacing the full kitchen.</p>
</article>
```

### Portfolio

[`portfolio.html`](portfolio.html) displays the project gallery with sixteen portfolio images and category labels for viewing all, cabinet, refinishing, and custom work. The current category controls are presentational links and do not filter the gallery without additional JavaScript or backend logic.

```html
<div class="menu">
  <a class="active" href="#">view all</a>
  <a href="#">cabinets</a>
  <a href="#">refinish cabinets</a>
  <a href="#">custom</a>
</div>
```

### Articles

[`articles.html`](articles.html) is the article index. It contains cabinet-related posts, dates, authors, summaries, read-more controls, and a category list. The current article links and read-more buttons are placeholders until article routing is connected.

```html
<article class="article_list">
  <h3><a href="articlesDetails.html">Cabinet Refacing in Las Vegas</a></h3>
  <p class="post_time">Dec, 24th 2018 | Posted By <span>admin</span></p>
  <button type="button">Read More</button>
</article>
```

### Article Details

[`articlesDetails.html`](articlesDetails.html) provides the full cabinet-refacing article view. It includes the article metadata, two supporting images, detailed copy, and the same article category sidebar used on the index page.

```html
<p class="post_time">Dec, 24th 2018 | Posted By <span>admin</span></p>
<p class="post_article">
  Refacing the cabinets of your Las Vegas kitchen is easy with Majestic
  Cabinets!
</p>
```

### Contact

[`contact.html`](contact.html) is the conversion page. It contains the consultation form, physical address, phone and fax details, website information, and an embedded Google Map. The form currently has no `action` endpoint, so it requires a backend or form provider before it can deliver submissions.

```html
<form action="/contact/" method="post">
  <input type="text" name="name" placeholder="Name" required />
  <input type="email" name="email" placeholder="Email" required />
  <textarea name="message" placeholder="Message" required></textarea>
  <input class="button" type="submit" value="Send Message" />
</form>
```

### Shared stylesheet and assets

[`style.css`](style.css) contains the shared layout and page-specific rules. Images are stored in [`images/`](images/) and referenced with relative paths from each HTML page.

```html
<link rel="stylesheet" href="style.css" />
<img src="images/logo.webp" alt="Majestic Cabinets logo" />
```

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

## Tools Setup

### Code editor

VS Code is recommended for editing HTML, CSS, and Markdown. Open the repository folder as a workspace so relative links and the `images/` directory are easy to inspect.

```bash
code Majestic-Cabinet
```

Useful extensions are optional: an HTML language-support extension, a CSS language-support extension, and a Markdown preview extension. The project does not require an extension to run.

### Git

Git is used to download and version the project. Verify the installation before cloning:

```bash
git --version
git clone <repository-url>
cd Majestic-Cabinet
git status
```

### Browser and developer tools

Use Chrome, Edge, Firefox, or another modern browser to inspect the pages. Browser developer tools are useful for checking responsive breakpoints, missing images, invalid markup, and console errors.

```text
Open a page in the browser
Right-click -> Inspect
Check Console for errors
Check Network for 404 asset requests
Toggle device emulation for mobile layouts
```

### Python static server

Python is optional, but its built-in HTTP server prevents common local path and asset issues that can occur when opening HTML files directly.

```bash
python --version
python -m http.server 8000
```

Stop the server with `Ctrl+C`. If port `8000` is busy, use another port:

```bash
python -m http.server 8080
```

### External font and icon tools

The pages load Google Fonts and Font Awesome from CDNs. An internet connection is required for those fonts and icons to appear. The HTML includes the Font Awesome stylesheet with an integrity value for safer loading.

```html
<link
  rel="stylesheet"
  href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.7.1/css/all.min.css"
/>
<i class="fa-solid fa-phone" aria-hidden="true"></i>
```

For an offline deployment, download and self-host approved font and icon assets, then replace the CDN links with local files.

### Image asset workflow

Keep image filenames stable because every page references them directly. Use WebP images where possible, provide meaningful `alt` text, and confirm every referenced file exists before deployment.

```text
images/
├── logo.webp
├── footer_logo.webp
├── portfolio1.webp ... portfolio16.webp
├── ourServices1.webp ... ourServices3.webp
└── articleDetails_img1.webp, articleDetails_img2.webp
```

### Optional Django tools

Django is only needed for server-side URL names, reusable templates, database-backed content, and working form submissions. It is not required for the current repository.

```bash
python -m venv .venv
\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install django
python -m django --version
```

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
