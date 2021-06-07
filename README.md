X FRONTEND TEST

### Requirements
- Have an account on [Docker Hub](https://hub.docker.com/)
- Have [Docker](https://docs.docker.com/engine/install/) installed
- Have [docker-compose](https://docs.docker.com/compose/install/) installed
- Do not have services running on the ports (9191, 8181, 8080 and 2222)

### Test

We will provide a docker image for you, this image will have an enviroment like we have on VIX. It will have:

- GITEA - software development version control.
- Staging Environment - When you merge something on master this environment will be updated whitin the master branch. (This is not your dev/local env.)
- Drone - Continuos Integration/Continuos Delivery
- SSH - Secure Shell 

### Step by Step

In order to proceed here you have to have all the [requirements](https://github.com/vixtech/mobile-test#requirements).

##### Clone the Repo

```bash
git clone https://github.com/vixtech/mobile-test.git
```

#### Run the docker image

Inside the project directory.
```bash
docker-compose up
```

#### Access all the services with your browser

- [Gitea](http://localhost:9191) (User: candidate, Password: changeit)
> The Gitea works like GitHub, you will use the provided user/password to login, and there you will have a repository with some issues to resolve. We expect that you create 1 Pull Request per issue. When all tests of the Pull Request CI/CD pass you can merge the PR yourself. We also expect that you match the PR in the issue and may update the issue with additional info. 
- [Staging enviroment](http://localhost:8181)
> All the code that is merged to master is deployed in this environment.
- [Drone](http://localhost:8080)
> Drone is our CI/CD application, it will run the pipeline for all commit we push to the repo.


#### After you solve the test

Commit the available container by just executing this command:

**Change the** `change-here-for-your-docker-hub-username` **for your docker-hub username**

```bash
docker commit $(docker ps | grep mobile-test | awk '{print $1}') change-here-for-your-docker-hub-username/mobile-test
```

Then make a docker login:

```bash
docker login
```

Then push the image.

**Change the** `change-here-for-your-docker-hub-username` **for your docker-hub username**

```bash
docker push change-here-for-your-docker-hub-username/mobile-test
```

Send us back 
