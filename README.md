# OpenRMF Documentation (v 0.13)

## Introduction to OpenRMF
OpenRMF is an open source tool for managing, viewing, and reporting of your DoD STIG checklists and Nessus Patch Scans in one web-based interface using your browser. It also generates a compliance listing of all your checklists across a whole system based on NIST 800-53 for your Risk Management Framework (RMF) documentation and process. This tool helps you manage multiple systems going through the RMF process and allows you to structure your data in a clean interface all in one location for your group or program. 

It will save you _weeks_ of manually checking vulnerability-to-CCI-to-NIST controls and manually generating reports, so you can get on to the value-added work for your cybersecurity hygiene.

When a team has poor visibility of their system’s risk data, it can result in bad decisions, errors, security risks and unforeseen issues. Teams must replace manual RMF and checklist methods that use spreadsheets and emails with an open, web-based solution that your team can leverage to plan, track and govern the entire RMF process. That is where OpenRMF helps you and your team!

Read more about its genesis <a href="https://www.cingulara.com/opensource.html" target="_blank">here</a>.

![Image](./img/UI-dashboard.png?raw=true)

## Current Functionality
- [x] Import SCAP scans (DISA STIGs) for automatic checklist documentation
- [x] Import Nessus ACAS scans (patches and updates) for automated reporting and managing critical updates
- [x] Exporting Nessus ACAS scans by host or total summary into MS Excel 
- [x] Dashboard showing # of open items per system and # Critical, High, Medium, and Low items from Nessus ACAS Scans
- [x] Generate a Compliance listing of NIST 800-53 Controls to all checklists within a system 
- [x] Filter the Compliance Generator for Low/Moderate/High projects as well as PII/Privacy overlay information
- [x] Save/Upload .CKL files for viewing and safekeeping
- [x] List and display active systems with checklists, scoring, and auditing information
- [x] List and display checklists with total open items and quick links to Vulnerabilities by status
- [x] List and display templated checklists (starting points)
- [x] Group and list checklists and reports by System (a group of checklists for a single application, system, etc.)
- [x] Reporting or "scoring" on Open, N/A, "Closed" as well as "not yet reviewed" items in the checklists quickly
- [x] Exporting the .CKL file for quick loading into the STIG Viewer Java application
- [x] Exporting checklists to MS Excel in seconds with color coded rows based on status (Open = RED, Not a Finding = GREEN, etc.)
- [x] Exporting of various charts for download to PNG
- [x] Filter Vulnerabilities on the Checklist page by status 
- [x] *Live Editing of Checklist data through the web browser*
- [x] Filter vulnerabilities for your Compliance listing based on major controls
- [x] Exporting your list of checklists and their score by status and category to MS Excel 
- [x] Metrics exported to Prometheus for API endpoints and NATS messaging, quickly display in Grafana
- [x] Single Docker Compose file to run locally
- [x] YAML to quickly setup this project in OpenShift or K8s natively
- [x] Interactive Nessus Report for searching on latest scan data, filtering, etc. via the web
- [x] Interactive Checklist Vulnerability report for search and filtering on vulnerabilities interactively via the web
- [x] User AuthN and AuthZ for login accounts and Role Based Access Control on functions
- [x] Auditing all creates, deletes, and updates
- [x] Import the Manual XML STIG to create a starting checklist (Automatic and behind the scenes for now)
- [x] *Generate the RMF POA&M*
- [x] Generate the Risk Assessment Report RAR
- [x] Generate the Test Plan
- [x] Central logging (ledger) for all CRUD and access usage based on NATS
- [x] Make the Keycloak setup easier (scripted)
- [x] Included Jaeger Tracing setup
- [x] Grafana and Prometheus included setup
- [x] External API access to certain functions in OpenRMF (ext-api-score)
- [x] Export Compliance Report to XLSX
- [x] Meaningful Health Checks in APIs and MSG clients

## ToDos (in no particular order)
- [ ] Performance improvements
- [ ] Separate Reporting API and Database (MSA)

If we are missing something you want, please add it on our main <a href="https://github.com/Cingulara/openrmf-web/issues" target="_blank">GitHub Issues</a> page.

## Description

The OpenRMF tool is an advanced alternative to the [DISA STIGViewer.jar](https://iase.disa.mil/stigs/Pages/stig-viewing-guidance.aspx) and MS Excel hell we go through used for DoD STIG checklist files, SCAP Scans, Nessus ACAS scans, RMF process information, and the like. It is necessary to capture and report on this information, please _do not_ mistake what I say for not agreeing with securing services. However, the DISA Java tool itself is horribly designed and not conducive to today's environment and use. And it is only part of the story. Their Java tool has been like this for a loooooonnnnnngggg time and I have wanted to make something better (IMO) for almost as long. So this tool here is the start! It is a way (currently) to view, report on, dive into, manage, and export your STIG checklists no matter which checklist you are referring to. All the .CKL files have a common format and htis reads and displays/manages that in a web front end using .NET Core APIs, MongoDB and NATS messaging. [View the history](https://www.cingulara.com/opensource.html) of this tool on our website. 

OpenRMF also is a single pane of glass for your DISA SCAP scans (to generate checklists), Nessus SCAP scans, Nessus patch scans (to track patch management), and compliance reporting for your systems going through the RMF process. We know: the RMF process is manual and all inclusive! This tool helps to automate as much as possible on the managing and reporting of data so you can:
1. Know your current Risk Profile
2. Know your current status
3. Know what is left to do
4. Know what your Critical and High items are so you can track and attack them

This particular repository is the repo for all the docs as the OpenRMF project goes along.  Documentation on the OpenRMF application will be here in MD files and reference images and other documents as well as GH markdown. This application idea has been brewing in my head for well over a decade and specifically since July 4th weekend 2018 when I started to put down code. Then in January 2019 when I scrapped all that July stuff and went for web APIs, microservices, eventual consistency, CQRS (command query responsibility segregation to scale separately), using MongoDB and NATS.

## What you need to run
You need a web browser that is fairly current. And you need Docker installed on your desktop (or Kubernetes/minikube) or server as this currently uses the Docker runtime to bring up all components with ` docker-compose ` via the included ".sh" shell (Linux / Mac) or ".cmd" command scripts (Windows).

* Docker is available at <a href="https://docs.docker.com/install/" target="_blank">https://docs.docker.com/install/</a>.

## Run OpenRMF locally
The best way to run this application (once you have Docker installed) is to go to the Code -- Releases tab https://github.com/Cingulara/openrmf-docs/releases and pull down the latest release. Unzip the file and then run the ./start.sh or .\start.cmd file to pull the latest images and run OpenRMF. Then you can open a local browser to http://{ip-address}:8080/ and see what happens. If you want to change the ports you only have to edit the docker-compose.yml file locally. These files are in the [scripts](scripts) folder of this repo.

Be sure to check out the [Keycloak information](#authentication-with-keycloak) because OpenRMF version 0.8 and beyond has RBAC for AuthN and AuthZ on the web and API calls. Or you could use another OpenID compliant application to provide AuthN and AuthZ. 

> You need to setup Keycloak first before running OpenRMF.

> The data is currently mapped to internal Docker-managed volumes for persistence. You can run the "docker volume rm" command below if you wish to remove and start over as you test.  If you want persistence you could change the connection strings to another MongoDB server and adjust the docker-compose.yml accordingly. Or use a volume in your docker-compose.yml or individual docker commands. 

> *_IMPORTANT:_* You must look at the .env file to see we set the Keycloak/OpenID location and realm. Check the `.env` file in the [scripts](scripts) directory to see how to set those variables. The docker-compose stack YML files read that .env file to launch. These cannot be "localhost" as "localhost" inside a docker container is that container, not the host it is running on.

```yaml
JWT-AUTHORITY=http://xxx.xxx.xxx.xxx:9001/auth/realms/openrmf
JWT-CLIENT=openrmf
```

## Run OpenRMF latest development
For those that want to run the actual "latest" or "edge" of OpenRMF you should run `git clone https://github.com/Cingulara/openrmf-docs.git `, then `git checkout develop` to switch to the develop branch. Inside the scripts directory there is an [edge](scripts/edge/) directory with ./dev-start.sh (or .\dev-start.cmd on Windows) file to run to start and a corresponding ./dev-stop.sh (.\dev-stop.cmd on Windows) to run the latest development version. These operate on http://{ip-address}:9080 so as not to interfere with a running released version to compare/contrast. Note the docker-compose.yml has different ports and different database mount volumes as well. 

> You must look at the YML files and see how we set the Keycloak/OpenID location and realm. Check the `.env` file in the [scripts](scripts) directory to see how to set those variables. The docker-compose stack YML files read that .env file to launch.

> Please ensure you check the launch.json on the VSCode windows to point to your NATS and your Keycloak setup.

## Install in Air-Gapped / Disconnected Environment

There are [separate instructions](airgapped-install.md) in the included air-gapped installation MD file.

## Metrics Tracking with Prometheus and Grafana

Starting with version 0.10.7 we include metrics tracking for all our major subsystems. See the [OpenRMF Metrics](metrics.md) document for more information.

## Authentication with Keycloak

Starting with version 0.8 we have AuthN and AuthZ setup for use. See the [Keycloak Document](keycloak.md) document for more information. 

> NOTE: You need to setup Keycloak before running OpenRMF. And you must get the .env file correctly setup.

## Creating MongoDB Users by Hand
If you wish you can create a MongoDB setup locally to persist your data and see what it does. Checkout the [create users by hand](create-users-by-hand.md) readme for more on that. 

## Cleaning up the Docker volumes and such every so often
If you want to remove all data from volumes you can run the below. Do at your own risk and know the consequences! I do this on my development machine to clear ALL volumes including those not for OpenRMF. 

* run `docker volume rm $(docker volume ls -qf dangling=true)` 
* run `docker system prune` and then enter `y` and press Enter when asked

## Screenshots of the UI

The OpenRMF Dashboard for all Systems
![Image](./img/UI-dashboard.png?raw=true)

The System Listing
![Image](./img/UI-system-listing.png?raw=true)

A System View
![Image](./img/UI-system-view.png?raw=true)

Exporting the Nessus Patch file summary to XLSX
![Image](./img/nessus-export-xlsx.png?raw=true)

The Individual Checklist view
![Image](./img/UI-checklist-scoring-vulns.png?raw=true)

Generate RMF Compliance Listing with linked Checklists and filtered vulnerabilities!
![Image](./img/UI-system-compliance-generator.png?raw=true)

The checklist Upload page
![Image](./img/UI-checklist-upload.png?raw=true)

Exporting the checklist to XLSX with color coding
![Image](./img/checklist-export-xlsx.png?raw=true)
