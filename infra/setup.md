# Setup for the AMM Techlab environment


## Policies

Script to give ServiceMonitor rights to hannelore's on their projects: [admin/service-monitor-rights.sh](./admin/service-monitor-rights.sh)


## Gitea Setup

If you want to pre-setup the Gitea users and repositories, follow these steps:

1. /sys spins up the AMM environment.
2. Register a Gitea User. The first registered user will be the Gitea Admin.
3. Create 15 hanneloreXY users.
4. Make a "Migration" repository for each user
    - Clone From URL <https://github.com/appuio/example-spring-boot-helloworld>
    - Owner hanneloreXY
    - example-spring-boot-helloworld
    - Visibility: [x] Make Repository Private

Steps 3 and 4 can be automated. See <https://{{% param techlabGiteaUrl %}}/api/swagger> for details on the API.


## Project cleanup

Script to delete all hannelore Projects: [admin/project-cleanup.sh](./admin/project-cleanup.sh)
