# DataElementHub Deployment

This repository contains everything that is required to deploy the [DataElementHub](https://dataelementhub.de/de/) metadata repository (MDR), developed by the [Institute for Medical Informatics](https://www.imi-frankfurt.de/) of the University Hospital Frankfurt.

## Deployment

1. Clone this git repository
2. Create your config file by copying the `.env.example` file to `.env`
3. Tailor configuration to your needs
    - Please make sure that you use an IP address / hostname for keycloak that can be reached from inside the docker container.
4. Setup Keycloak. You might want to use the provided example profiles. 
    - `dehub.json` contains the client profile for authentication using the GUI.
    - `dehub-api.json` contains a profile that you may use in your applications for access to the REST API.
5. Start DataElementHub using `docker-compose up -d`
    - The first startup will take a few minutes, as both docker images are built on the fly.

## Keycloak configuration

The DataElementHub relies on Keycloak for authentication.
Data access is granted by being a member of the realm. 

Apart from that, DataElementHub currently has the role `createNamespace` that needs to be created on the `dehub` client assigned to users.

:warning: The current version has the `/auth` prefix as part of the Keycloak URL hard wired ([see my PR](https://github.com/mig-frankfurt/dataelementhub.gui/pull/60)). If you're running a recent version of Keycloak that comes without the `/auth` prefix, you will run into problems.

## Source code

I am not part of the aforementioned Insitute of Medical Informatics, neither am I a developer of DataElementHub. Therefore this deployment methed is to be consideres as *unofficial*.

The source code of DataElementHub is available [here](https://github.com/mig-frankfurt).