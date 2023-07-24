# arches_for_science_package

### This is a version of the Arches for Science project that has been modified to work with the `installed packages` branch ( https://github.com/archesproject/arches/pull/9426 )

##### Setup
1.  ( if working locally ) run `pip install .` inside package to copy files into ENV
2.  create a project
```
arches-project create $PROJECT_NAME
```
3. add package to INSTALLED_APPS and INSTALLED_PACKAGES
4. add package to dependencies in package.json
```
"dependencies": {
 "arches": "archesproject/arches#stable/7.4.0",
"arches_for_science_package": "archesproject/arches_for_science_package"
}
```
5. update project settings.py with anything from installed_package settings.py
```
ELASTICSEARCH_HOSTS = [{"scheme": "http", "host": "localhost", "port": ELASTICSEARCH_HTTP_PORT}]
TEMPLATES[0]["OPTIONS"]["context_processors"].append("arches_for_science_package.utils.context_processors.project_settings")
APP_TITLE = "Arches for Science"
COPYRIGHT_TEXT = "All Rights Reserved."
COPYRIGHT_YEAR = "2019"


CELERY_BROKER_URL = "amqp://guest:guest@localhost"
CELERY_ACCEPT_CONTENT = ["json"]
CELERY_RESULT_BACKEND = "django-db"  # Use 'django-cache' if you want to use your cache as your backend
CELERY_TASK_SERIALIZER = "json"
ONTOLOGY_NAMESPACES = {
    "http://purl.org/dc/terms/": "dcterms",
    "http://purl.org/dc/elements/1.1/": "dc",
    "http://schema.org/": "schema",
    "http://www.w3.org/2004/02/skos/core#": "skos",
    "http://www.w3.org/2000/01/rdf-schema#": "rdfs",
    "http://xmlns.com/foaf/0.1/": "foaf",
    "http://www.w3.org/2001/XMLSchema#": "xsd",
    "https://linked.art/ns/terms/": "la",
    "http://www.w3.org/1999/02/22-rdf-syntax-ns#": "rdf",
    "http://www.cidoc-crm.org/cidoc-crm/": "",
    "http://www.ics.forth.gr/isl/CRMdig/": "",
    "http://www.ics.forth.gr/isl/CRMgeo/": "geo",
    "http://www.ics.forth.gr/isl/CRMsci/": "sci",
}




RENDERERS += [
    {
        "name": "fors-reader",
        "title": "ASD Hi Res FieldSpec4",
        "description": "Use for exports from all our ASD High Resolution Field Spectroscopy",
        "id": "88dccb59-14e3-4445-8f1b-07f0470b38bb",
        "iconclass": "fa fa-bar-chart-o",
        "component": "views/components/cards/file-renderers/fors-reader",
        "ext": "txt",
        "type": "text/plain",
        "exclude": "",
    },
    {
        "name": "xrf-reader",
        "title": "HP Spectrometer XRF ASCII Output",
        "description": "Use for exports from all our HP XRF outputs",
        "id": "31be40ae-dbe6-4f41-9c13-1964d7d17042",
        "iconclass": "fa fa-bar-chart-o",
        "component": "views/components/cards/file-renderers/xrf-reader",
        "ext": "txt",
        "type": "text/plain",
        "exclude": "",
    },
    {
        "name": "raman-reader",
        "title": "Raman File Reader",
        "description": "Use for exports from all our HP raman and gas chromatograph spectrometers",
        "id": "94fa1720-6773-4f99-b49b-4ea0926b3933",
        "iconclass": "fa fa-bolt",
        "component": "views/components/cards/file-renderers/raman-reader",
        "ext": "txt",
        "type": "text/plain",   
        "exclude": "",
    },
    {
        "name": "pdbreader",
        "title": "PDB File Reader",
        "description": "",
        "id": "3744d5ec-c3f1-45a1-ab79-a4a141ee4197",
        "iconclass": "fa fa-object-ungroup",
        "component": "views/components/cards/file-renderers/pdbreader",
        "ext": "pdb",
        "type": "",
        "exclude": "",
    },
    {
        "name": "pcdreader",
        "title": "Point Cloud Reader",
        "description": "",
        "id": "e96e84f2-bcb2-4ca4-8793-7568b09d7374",
        "iconclass": "fa fa-cloud",
        "component": "views/components/cards/file-renderers/pcdreader",
        "ext": "pcd",
        "type": "",
        "exclude": "",
    },
    # {
    #     "name": "colladareader",
    #     "id": "3732bdf0-74b1-412f-955a-9ca038e7db31",
    #     "iconclass": "fa fa-spoon",
    #     "component": "views/components/cards/file-renderers/colladareader",
    #     "ext": "dae",
    #     "type": "",
    #    "exclude": [],
    # },
]


X_FRAME_OPTIONS = "SAMEORIGIN"


FORMATS = [
    {"name": "Bruker M6 (point)", "id": "bm6", "renderer": "31be40ae-dbe6-4f41-9c13-1964d7d17042"},
    {"name": "Bruker 5g", "id": "b5g", "renderer": "31be40ae-dbe6-4f41-9c13-1964d7d17042"},
    {"name": "Bruker Tracer IV-V", "id": "bt45", "renderer": "31be40ae-dbe6-4f41-9c13-1964d7d17042"},
    {"name": "Bruker Tracer III", "id": "bt3", "renderer": "31be40ae-dbe6-4f41-9c13-1964d7d17042"},
    {"name": "Bruker 5i", "id": "b5i", "renderer": "31be40ae-dbe6-4f41-9c13-1964d7d17042"},
    {"name": "Bruker Artax", "id": "bart", "renderer": "31be40ae-dbe6-4f41-9c13-1964d7d17042"},
    {"name": "Renishaw InVia - 785", "id": "r785", "renderer": "94fa1720-6773-4f99-b49b-4ea0926b3933"},
    {"name": "Ranishsaw inVia - 633/514", "id": "r633", "renderer": "94fa1720-6773-4f99-b49b-4ea0926b3933"},
    {"name": "ASD FieldSpec IV hi res", "id": "asd", "renderer": "88dccb59-14e3-4445-8f1b-07f0470b38bb"},
]

```
6. update urls to include installed_package
```
urlpatterns = [
    url(r'^', include('arches.urls')),
    url(r"^", include("arches_for_science_package.urls")),
    path("reports/", include("arches_templating.urls")),
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```
7. update INSTALLED_APPS with anything that was in package
```
INSTALLED_APPS = (
    "webpack_loader",
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",
    "django.contrib.gis",
    "arches",
    "arches.app.models",
    "arches.management",
    "guardian",
    "captcha",
    "revproxy",
    "corsheaders",
    "oauth2_provider",
    "django_celery_results",
    "compressor",
    # "silk",
    "$PROJECT_NAME",
    "arches_for_science_package",
    "arches_templating",
)
```
8. install the package
```
python manage.py packages -o load_package -s /Users/cbyrd/Projects/ENV/lib/python3.8/site-packages/arches_for_science_package/pkg -dev  -y -db
```
9. Run the project
