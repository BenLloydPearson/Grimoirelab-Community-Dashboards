# Grimoirelab Dashboards
> Visualization dashboards for [Grimoirelab](https://github.com/chaoss/grimoirelab), provided by the Grimoirelab Community

This is a collection of Grimoirelab Dashboards designed to help identify and solve problems within open source software development communities by gathering data from multiple community data sources.
 

## Table of Contents

- [Background](#background)
- [Install](#install)
- [Usage](#usage)
- [Contribute](#contribute)
- [License](#license)

## Background

[Grimoirelab](https://github.com/chaoss/grimoirelab) is part of a suite of software analytics tools that index data from various software development resources (GitHub/GitLab, Jira, Gerrit, etc.) in Elasticsearch, and produce visualizations with Kibana. This is a collection of Dashboards for use with Kibiter, the custom version of Kibana that is deployed for Grimoirelab. These dashboards are designed to help you identify and solve specific problems within your open source community and are more focused than the general metrics that are provided by default in Grimoirelab.

## Install
If you're not familiar with Grimoirelab, [please read the official tutorial](https://grimoirelab.gitbooks.io/tutorial/) to familiarize yourself with how it works. Then, you'll need to setup a full installation of all of it's components. The easiest method is to [deploy it in  a Docker container](https://grimoirelab.gitbooks.io/tutorial/mordred/mordred-in-a-container.html).

For convenience, this repo includes everything you need to generate a simple dashboard. Ensure you have [docker-compose installed on your device](https://docs.docker.com/compose/install/), then run the following command from inside this repository.

`docker-compose up -d`

This will setup a [grimoirelab/full container](https://hub.docker.com/r/grimoirelab/full/) and configure it to use these dashboards.

To view the dashboards, open your web browser and navigte to http://localhost:5601

If you use another method, you'll need to configure Kibiter to use config/menu.yaml and the dashboards found in the panels directory. Please review the [Grimoirelab Tutorial](https://grimoirelab.gitbooks.io/tutorial/grimoireelk/intro.html) for more information about this.

## Usage

Dashboard configuration can be found in [config/menu.yaml](./config/menu.yaml). This is where you will modify the dashboards you want to display. To add or remove project data, modify [config/projects.json](./config/projects.json). There are more configuration options provided inside the config directory, for more details on them please [refer to the Grimoirelab tutorial section on Mordred](https://grimoirelab.gitbooks.io/tutorial/mordred/intro.html).

Whenever you modify these configuration files, make sure you restart the container for the changes to take effect.

If you want to save changes to the dashboard so the persist across container restarts, you need to get a shell environment inside the docker container and use kidash to export the necessary information, then you need to copy that data to your host machine. If you are using the docker configuration provided in this repo, here is how to do it.

```
docker exec -ti grimoirelab_dashboards env /bin/bash
kidash -e http://localhost:9200 --dashboard "Your-Dashboard-Title" \
  --export /tmp/your-dashboard-title.json
exit
docker cp grimoirelab_dashboards:/tmp/your-dashboard-title.json panels/your-dashboard-title.json 
```

## Contribute

Please refer to [the contributing.md file](Contributing.md) for information about how to get involved. We welcome issues, questions, and pull requests. Pull Requests are welcome.

## Maintainers
Ben Lloyd Pearson: ben.pearson@oath.com

## License

This project is licensed under the terms of the [MIT](LICENSE-MIT) open source license. Please refer to [LICENSE](LICENSE) for the full terms.


