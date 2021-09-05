# Welcome DevOps Engineers !

This repository is built by the community, for the community. It defines the journey for all new Devops folks who want to get started with DevOps tools and Technologies

## Which platform does it uses?


It is based on [Docsy](https://github.com/google/docsy) tool. It is a Hugo theme for technical documentation sites, providing easy site navigation, structure, and more. 

## How to contribute?

###  Clone this repository with all the submodules


```bash
git clone --recurse-submodules --depth 1 https://github.com/collabnix/community
```

### Install the dependencies

```bash
npm install
```

### Running the website locally



Once you've made your working copy of the site repo, from the repo root folder, run:

```
hugo server
```

Visit https://localhost:1313

## Running a container locally

You can run docsy-example inside a [Docker](https://docs.docker.com/)
container, the container runs with a volume bound to the `docsy-example`
folder. This approach doesn't require you to install any dependencies other
than [Docker Desktop](https://www.docker.com/products/docker-desktop) on
Windows and Mac, and [Docker Compose](https://docs.docker.com/compose/install/)
on Linux.

1. Build the docker image 

   ```bash
   docker-compose build
   ```

1. Run the built image

   ```bash
   docker-compose up
   ```

   > NOTE: You can run both commands at once with `docker-compose up --build`.

1. Verify that the service is working. 

   Open your web browser and type `http://localhost:1313` in your navigation bar,
   This opens a local instance of the docsy-example homepage. You can now make
   changes to the docsy example and those changes will immediately show up in your
   browser after you save.

### Cleanup

To stop Docker Compose, on your terminal window, press **Ctrl + C**. 

To remove the produced images run:

```console
docker-compose rm
```
For more information see the [Docker Compose
documentation](https://docs.docker.com/compose/gettingstarted/).

## Troubleshooting

As you run the website locally, you may run into the following error:

```
➜ hugo server

INFO 2021/01/21 21:07:55 Using config file: 
Building sites … INFO 2021/01/21 21:07:55 syncing static files to /
Built in 288 ms
Error: Error building site: TOCSS: failed to transform "scss/main.scss" (text/x-scss): resource "scss/scss/main.scss_9fadf33d895a46083cdd64396b57ef68" not found in file cache
```

This error occurs if you have not installed the extended version of Hugo.
See our [user guide](https://www.docsy.dev/docs/getting-started/) for instructions on how to install Hugo.


### I have an idea. How shall I share?

Visit [Collabnix Slack](https://launchpass.com/collabnix) and share your ideas under #contribute channel


