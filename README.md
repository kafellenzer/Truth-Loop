[hi-level-arch]: images/architectural-diagram.png "High Level Architecture"
[components]: images/components.jpg "Components"
[openshift]: images/openshift.png "OpenShift Console"
[dataflow]: images/dataflow.png "Data flow"

# Truth-Loop

The initial version was developed by contributors at IBM in the summer of 2020, namely: Aakansha Agrawal, Khadija Al-Selini, Parisa Babaali, Boz Bosma, Kimberly Cassidy, Stephanie Daher, Michelle Esselen, Peter Ihlenfeldt, Abiola Jones, Rahul Kalluri, Joe Konathapally, Frank Madden, Henry Nash, Sharon Osahon, Colby Stone, Mark Sturdevant, Tanushree Paul, Bimsara Pilapitiya, Ya Jiao Zheng.

## Current Forked Repository

The forked version of Truth Loop located in this GitHub repository was made to restructure the content management system (CMS). Currently, Truth Loop utilizes both Watson Media as its CMS and PostgreSQL as the relational database management server (RDMS). Both of these require a subscription to utilize which could limit its availability to the public. Our goal is to replace these servers with a CMS and RDMS that are free to use. At the moment, the best option that we have found is [Concrete5](https://www.concrete5.org/about/feature-index). Not only is it a cheaper option, but also Concrete5 requires a MySQL (with PHP data object extensions) RDMS. This also partly addresses issues brought up concerning expanding support of multiple RDMSs. 

Throughout this README document, the original Truth Loop documentation will be replaced in areas where our contributors have adjusted specific aspects. Any questions or concerns can be addressed by the following contributors:
- Escher Campanella at campae@rpi.edu 
- Kelly Fellenzer at fellek@rpi.edu

## Contents

1. [Overview](#Overview)
   1. [What's the Problem?](#whats-the-problem)
   1. [How can technology help?](#how-can-technology-help)
1. [The Idea](#the-idea)
1. [Previous Design and Diagrams](#previous-design-and-diagrams)
2. [Our Proposition for Concrete5](#our-proposition-for-concrete5)
3. [Video](#Video)
4. [Technologies](#Technologies)
5. [Getting Started](#Getting-started-by-installing-and-running-the-components)
6. [Docker](#Running-on-Docker)
7. [Resources](#Resources)
8. [License](#License)
9. [Contributing and Developer information](#Contributing-and-Developer-information)
    1. [Future Enhancements to the Solution](#future-enhancements-to-the-solution)
    1. [Privacy Considerations](#Privacy-Considerations)

## Overview

### What's the problem?

Concerned and impacted citizens don't have a straightforward way of knowing
what or how policies, regulations, and legislation (throughout this document
referred as either **Legislative Artifacts** or **PR&L**) impact them or
how they can share their approval, concerns, and/or questions with lawmakers.

### How can technology help?

What is missing to help communities contribute their feedback related to PR&L, and what this technology was intending to provide, is a means for people to:

- readily understand the PR&L language and intent without being a legal expert
- sort or filter the PR&L efficiently
- digest an understandable summary of PR&L
- explore related or supporting information, advocacy groups, and other PR&L
- make a determination of whether the PR&L will impact them
- engage in the process of providing feedback about PR&L
- communicate the potential effects of these PR&L on their life, family, or community
to the author or sponsor of the legislation
- share their stories and experiences with fellow residents and policy makers
- see what other people in the community are saying
- get an idea of the general sentiments people have expressed about the PR&L
- engender dialogue between residents, PR&L authors, and sponsors

## The Idea

The driving idea behind the software is to provide a platform that is capable of storing
curated PR&L information, as determined by the community (however large or small) it serves.
The platform provides a mobile-friendly way for users to examine PR&L, helping increase
their legal awareness and allowing them to communicate their reactions and thoughts with
video testimonials.  These testimonials are then shared with the community and those
responsible for the creation of the PR&L.

## Previous Design and Diagrams

![architecture diagram](/images/high-level-architecture-diagram.png)

This solution combines a media server (currently Watson Media) and distributed database service to hold the curated legislative artifacts and the related metadata.

- The user launches the web app (on either a laptop, desktop, or mobile device) and can view the range of curated legislative artifacts (1). The Vue app retrieves these by sending a REST request to the API server, which extracts them (3) from the SQL database.
- The user can post their own (video) story to support or challenge the legislated artifacts to the API server, which directs it to the Watson Media services (2). The API server also stores a reference to the video location in the respective legislative artifact in the SQL database (3).
- The user can view other peoples' video stories which are retrieved by sending a REST request to the API server, which, after looking up the ID of the video in the SQL database (3), extracts them from Watson Media services (2).

There is an administrative API interface that allows the site owners to curate the PR&L information, with the following attributes:

- a simple, intelligible summary that makes it easy to understand its potential impact
- categories it pertains to (law enforcement, healthcare, zoning)
- geospatial areas of pertinence (postal codes, cities, counties, and so on)
- the type of the artifact (bill, law, policy, regulation, and so on)
- related PR&L in the system
- legislator, author, and sponsor of the PR&L
- related advocacy groups or digital social communities
- related articles or supporting documentation
- a link to the full text of the PR&L

## Our Proposition for Concrete5

![new architecture diagram](/images/conceptualmodel.png)

Our new proposed solution combines Concrete5 as the media server and MySQL satabase service to document and manage various legislative artifacts and the related metadata. As you can see in this diagram, there are additional RDMSs that Concrete5 has the ability to utilize, however, for our scope of this project we are not concerned with making sure they are implemented fully. 

## Video

[![Video Call for Code for Racial Justice Solution Starter: Truth Loop ](https://img.youtube.com/vi/AgTUXp4G1Ms/0.jpg)](https://www.youtube.com/watch?v=AgTUXp4G1Ms)

## Technologies

- [IBM Cloud Documentation Home](https://cloud.ibm.com/docs/home/alldocs)
- [Kubernetes in IBM Cloud](https://cloud.ibm.com/docs/containers?topic=containers-cs_cluster_tutorial)
- [PostgreSQL](https://cloud.ibm.com/docs/databases-for-postgresql?topic=databases-for-postgresql-getting-started)
- [OpenShift](https://cloud.ibm.com/docs/openshift?topic=openshift-getting-started)
- [Node.js](https://nodejs.org/en/docs/)
- [ExpressJS](https://expressjs.com/)
- [Vue.js](https://vuejs.org/)

## Getting started by installing and running the components

### Prerequisites

- Register for an [IBM Cloud](https://www.ibm.com/account/reg/us-en/signup) account.
- Install and configure [IBM Cloud CLI](https://cloud.ibm.com/docs/cli?topic=cloud-cli-getting-started#overview).
- Install [Vue CLI dependencies](https://cli.vuejs.org/guide/installation.html)
- Clone the [repository](https://github.com/Call-for-Code-for-Racial-Justice/Truth-Loop).

### Steps

1. [Provision a MySQL instance on the IBM Cloud](#1-Provision-a-MySQL-instance).
1. [If you want to use the video services, provision an instance of Concrete5](#2-Set-up-an-instance-of-Concrete5).
1. [Configuring and run the server](#3-Configuring-and-running-the-server).
1. [Configuring and run the client application](#4-Configuring-and-running-the-client-application).

### 1: Deploy a MySQL database

#### Using the IBM Cloud:

You can deploy this in the IBM Cloud by logging into to IBM Cloud and Composing a [MySQL database](https://cloud.ibm.com/catalog/services/compose-for-mysql). Note that this does requre a paid plan, however if you have just signed up for a new IBM CLoud account, you will have received cloud credits, which would gover this for some time.

#### Deploying locally:

Alternatively, you could set up your own MySQL database locally. MySQL Community is the feely downloadable version of MySQL. It is available under the GPL license and is supported by a huge and active community of open source developers. To view the options for dowloading the MySQL community software, visit the link [here](https://dev.mysql.com/downloads/), and to read about what the software can provide, visit the link [here](https://www.mysql.com/products/community/).

Before you start downloading this, you'll have to make an account on Oracle [here](https://profile.oracle.com/myprofile/account/create-account.jspx?pid=mysql&nexturl=https%3A%2F%2Floginmysql.oracle.com%2Fauth%2Fslogin%2F%3Ftoken%3D525445df6TGdjgS11krEZSv3QAQBtPscvigiIfq0s3dD_VnekvT8wdu1nXgyQ4uLUjKK_DXhwJVxGAbFmAOF97YX8T8OBcY4z9LAm-owcMMT8ItR8Do4cyvanD9A4GzugMIlBXeiFM28s8vVsWAVaEv5uggeRkqq762wYnjFDov5iAEmCKGulXf6o1NPYzUaLzCFbVQOmlVN28naEO7Q8HFuNLVaWiEGYHunHQjvp1zK8K3scs8.).

### 2. Set up an instance of Concrete5



### 3. Configuring and running the server

To set up and launch the server application:

1. Go to the `server` directory of the cloned repo.
1. Copy the `.env.example` file, and create a new file named `.env`.
1. If your PostgreSQL server uses SSL (like the IBM Cloud version), then create a file named `cert.pem` to hold the SSL certificate. For the IBM Cloud version of PostgreSQL, it is shown in the `certificate: certificate_base64` attribute of the service credential you obtained in [Step 1](https://github.com/Call-for-Code-for-Racial-Justice/Truth-Loop#1-Provision-a-Postgres-instance). Copy the raw contents of this attribute into the file you have created.

1. Update the newly created `.env` file and update the `DB_HOST`, `DB_USERNAME`, `DB_PASSWORD`, `DB_PORT` and `DB_DATABASE_NAME` with the values from the credentials you obtained in [Step 1](https://github.com/Call-for-Code-for-Racial-Justice/Truth-Loop#1-Provision-a-PostgreSQL-instance). If you created a certificate file in the previous action, then also update the `DB_CERTFILE` with the location of this file (relative to the `server` directory). For example, `DB_CERTFILE=./cert.pem`.
1. Also update the `CMS_USERNAME`, `CMS_PASSWORD`, `CLIENT_ID` and `CLIENT_SECRET` with the values from creating your instance of Watson Media, from [Step 2](https://github.com/Call-for-Code-for-Racial-Justice/Truth-Loop#2-Set-up-an-instance-of-Watson-Media). 

 1. Prepare to initialize the database with the correct tables. Scripts are provided that do this using the  `psql`  CLI, which is recommended that you install:
	- macOS:	
        -   `brew install libpq`
        -   You may also like to link the  `psql`  command to you local bin directory with brew  `link --force libpq`

	- Windows:
        - Download PostgreSQL for Windows [here](https://www.postgresql.org/download/windows/).
        - You will also need to add the path to your PostgreSQL bin directory to your PATH variable in order for the CLI to work.

1. To initialize the tables, you can use the `./psql_create_tables.sh` script
1. If you would like to install sample data into the database for testing, then use the `./psql_refresh_sample_data.sh` script

1. To run the server, from a terminal, in the `server` directory of the cloned repo:
    1. Install the dependencies: `npm install`
    1. Launch the server application locally or deploy to IBM Cloud:
        - To run locally:
            1. Start the application: `npm start`
            1. The server can be accessed at the address give, typically <http://localhost:5000>
        - To deploy to the IBM Cloud in Cloud Foundry:
            1. Edit the **name** value in the `manifest.yml` file to a unique application name (for example, _my-legislative-server_).
            1. Log in to your IBM Cloud account using the IBM Cloud CLI: `ibmcloud login`
            1. Target a Cloud Foundry org and space: `ibmcloud target --cf`
            1. Push the app to IBM Cloud: `ibmcloud app push`
            1. The server can be accessed at the  **routes** URL displayed in the output of the push command (for example: <my-legislative-server.eu-gb.mybluemix.net>)

Once the server is running, you can test it by accessing the openAPI docs interface using the `/api-docs` endpoint. For example, if running locally this will be on <http://localhost:5000/api-docs>, which should look something like this:

![api-docs](/images/api-docs.png)

### 4. Configuring and running the client application

To configure and run the client application:

1. Go to the `client` directory of the cloned repo.
1. Copy the `.env.example` file to a new file named `.env`
1. Edit the newly created `.env` file:
    - Update the `SERVER_URL` with the URL to the server app launched in the previous step (for example <http://localhost:5000>).
1. From a terminal:
    1. Install the dependencies:
        - `npm install`
        - `npm run serve`
    1. Once the development server is running, you should be able to access the client from the URL indicated (typically <http://localhost:8080/>)
    1. If you are running a mobile simulator, you can also access the same URL. For example, in the ios simulator, the screen would look something like this:

![Intro Screen](/images/first-screen.png)

## Running on Docker

Running Truth Loop components as containers allows a simple and fast set-up of the application.

### Pre-requisites

- Install [Docker](https://docs.docker.com/get-docker/)
- Install [Docker Compose](https://docs.docker.com/compose/install/)

### Steps

1. Ensure that your `docker-compose.yml` is up to date with the components you wish to run.
1. In a terminal, navigate to the `server` directory and run `docker-compose up -d --build`.
1. Check that all containers are up and running by issuing `docker ps -a`.
1. Access each as normal component via their `localhost` ports.
1. Once finished, run `docker-compose down`.

## Resources

- Any non-tech resources go here (e.g. links/videos to legislation, and the problem being solved)

## License

This solution is made available under the [Apache 2 License](LICENSE).

## Contributing and Developer information

The community welcomes your involvement and contributions to this project. Please read [contributing](CONTRIBUTING.md) for details on our code of conduct, and the process for submitting pull requests to the community.

### Future Enhancements to the Solution

There are a significant number of areas where the community is looking for help. Individual issues are raised in the repository, but the following class of assistance is needed:

- **Media services:** The current approach supports only one media service, Watson Media. Although this provides excellent capabilities, there is a desire to support a broader range of media services for testimonial videos. Various approaches have been researched, including use of a non-streaming solution using Cloud Object Storage to call stored videos to be downloaded and then played back to the user upon loading of the page. As the videos will have a restriction of 60 second time limits, optimization can be made to minimize the overhead of waiting to download the entire video before playback. This implementation is certainly feasible, however it is not scalable when taking into account users with potentially weaker network connections.
- **Security:** An efficient expansion to secure data storage (particularly regarding the video implementation) is required to ensure all user data is kept safe. Implementation of user accounts that safely store user data may even assist in developing a more convenient solution, however the privacy implications that come with this should also be assessed.
- **Privacy considerations around videos and location information:** Consideration of the metadata around user testimonials will be essential in providing a solution that focuses on privacy risks.
- **Sourcing legislation information:** Several data sources will be required to adapt the solution for all locales, therefore expansion of this project will be impacted massively by taking into account the structures of legislation from other countries.
- **Policy upload and curation:** Thought needs to be given to who would curate the policy data. Would the database population of policy data be automated to pull all newly proposed policies from government sources, requiring an interface to filter suitable policies to then be pushed into the database? Or would the curation be done manually, which allows for more control with the drawback of lower scalability?
- **Moderation of uploaded videos/text:** How is video or accompanying text reviewed to ensure community guidelines are being followed, and that users are not misusing the application? Applications of moderation can include profanity detection, manual moderation via user admins, or through flagging and reporting of user content. Furthermore, consideration should be made to assess whether these implementations address the spirit of the solution, e.g. how to distinguish this software from social media settings where users already share political views.
- **Natural language technology:** Work has already begun on refining a pipeline to extract text from video submissions to implement tone analysis, which will help to identify various characteristics and give more meaning to the video testimonials from users. Further expansion can be made to analyze profanity and inappropriate language submitted by users, to address moderation of user content.

### Privacy Considerations for Implementors

Due to the nature of the solution, Personal Information (PI) could be prevalent within an implementation of a Truth Loop system. For implementors, there are a number of important considerations to take into account. Please refer to the [Platform Privacy Statement](privacy/platform_privacy_statement.md) and [Application User Guide](privacy/app_user_guide.md) documents to help you with your implementation.
