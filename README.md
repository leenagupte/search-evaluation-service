# search-evaluation-service

Evaluation service for [search-api-v2](https://github.com/alphagov/search-api-v2).

This app run evaluations for [GOV.UK site search](https://www.gov.uk/search/all) using the Google Vertex AI Search evaluations framework

## Nomenclature

### "Vertex" vs "Discovery Engine"
The marketing name of the search product we use (Google Vertex AI Search) has undergone several changes, and some concepts have different naming in the Google Cloud Platform UI compared to the actual underlying APIs themselves.

We have chosen to exclusively use the more stable API naming (Discovery Engine, engine instead of app, etc.) throughout the codebase and documentation to avoid having to rename things as the product reached general availability, but you may see the terms "Vertex" or "Vertex Search" as well as some other marketing terms used in some project artefacts.

## Technical documentation

### Local development

The official way of running this application locally is through [GOV.UK Docker](https://github.com/alphagov/govuk-docker), where a project is defined for it. Because this application is deeply integrated with a SaaS product, you will have to have access to a GCP Discovery Engine engine to be able to do anything more meaningful than running the test suite. govuk-docker will do this for you by configuring the environment to point to integration. If you want to run the application without GOV.UK Docker, you can reference the required [environment variables](https://github.com/alphagov/govuk-docker/blob/main/projects/search-evaluation-service/docker-compose.yml) from there.

You can run the application from within the govuk-docker repository directory as follows:

### Building search-evaluation-service

```bash
make search-evaluation-service
```

### Running the test suite

```bash
govuk-docker run search-evaluation-service-lite bundle exec rake
```

### Running rake tasks

Rake tasks can be run against the `task-runner` stack:

```bash
govuk-docker run search-evaluation-service-task-runner bundle exec rake [relevant-rake-task]
```

Alternatively, you can run the `lite` stack, setting additional environment variables to point to integration:

```bash
govuk-docker run search-evaluation-service-lite env GOOGLE_CLOUD_PROJECT_ID="780375417592" DISCOVERY_ENGINE_DEFAULT_COLLECTION_NAME="projects/780375417592/locations/global/collections/default_collection" DISCOVERY_ENGINE_DEFAULT_LOCATION_NAME="projects/780375417592/locations/global" bundle exec rake [relevant-rake-task]`
```

Note that when rake tasks are run locally, no metrics will be pushed to Prometheus. This is because the Prometheus push gateway is local to the cluster in integration, staging or production. If you need metrics to be pushed to Prometheus, run the task in the relevant cluster.

### Further documentation

[Google Vertex docs](https://cloud.google.com/generative-ai-app-builder/docs/introduction)

## Licence

[MIT Licence](LICENCE.txt)
