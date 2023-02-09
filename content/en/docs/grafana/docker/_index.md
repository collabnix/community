---
title: "How to Run Grafana in a Docker container"
linkTitle: "How to Run Grafana in a Docker container"
weight: 330
date: 2023-02-09
description: >
 Running Grafana in a Docker Container 
---

Running Grafana in a Docker container is a straightforward process that can be done using the following steps:

- Pull the Grafana Docker image: To get started, you'll need to pull the Grafana Docker image from the Docker Hub repository. This can be done using the following command:
bash

```
docker pull grafana/grafana
```

- Start the Docker container: Once the image is pulled, you can start a new Docker container using the following command:
bash


```
docker run -d -p 3000:3000 grafana/grafana
```

The -d option runs the container in the background, and the -p 3000:3000 option maps the Grafana server port (3000) to the host machine.

- Access the Grafana web interface: After starting the Docker container, you can access the Grafana web interface by navigating to http://localhost:3000 in your web browser.

- Log in to Grafana: The first time you access the Grafana web interface, you'll need to log in using the default username (admin) and password (admin). You can then change these credentials in the Grafana settings.

- Configure data sources: Once logged in, you can add and configure data sources for Grafana to connect to. This can be done using the "Data Sources" menu in the Grafana web interface.

- Create dashboards: You can create dashboards to visualize and analyze your data by using the "Dashboards" menu in the Grafana web interface.

That's it! You should now have Grafana running in a Docker container, and be able to access the Grafana web interface to start visualizing and analyzing your data.

Note: If you are running Grafana in a production environment, you should consider using a more secure setup, such as using a reverse proxy and securing access to the Grafana web interface using SSL/TLS. Additionally, you should also ensure that you are using the latest version of Grafana and keep it up to date to ensure that you have access to the latest security updates and features.
