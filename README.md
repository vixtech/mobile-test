# MOBILE TEST

### Requirements
- Have an account on [Docker Hub](https://hub.docker.com/)
- Have [Docker](https://docs.docker.com/engine/install/) installed
- Have [docker-compose](https://docs.docker.com/compose/install/) installed
- Do not have services running on the ports (9191, 8181, 8080 and 2222)

### Test Summary

We will provide a docker image for you, this image will have an enviroment like we have on VIX. It will have:
- GITEA - software development version control. - Staging Environment - When you merge something on master this environment will be updated whitin the master branch. (This is not your dev/local env.)
- Drone - Continuos Integration/Continuos Delivery
- SSH - Secure Shell 

The Gitea works like GitHub, you will use the provided user/password to login. Inside Gitea you will find a repository with some issues to resolve. 
We expect that you create 1 Pull Request per issue. When every PR CI/CD test pass you can merge it by yourself. 

After you are done you have to submit the image back to us.

---

### Step by Step

1. Make sure you are ready

In order to proceed to the next step you must have all the [requirements](https://github.com/vixtech/mobile-test#requirements).

2. Clone the Repo

```bash
git clone https://github.com/vixtech/mobile-test.git
```

3. Run the docker image inside the project directory

```bash
docker-compose up

```

4. Verify you can access all the services with your browser:

- [Gitea](http://localhost:9191):  User: candidate, Password: changeit
- [Staging enviroment](http://localhost:8181): All the code that is merged to master is deployed in this environment.
- [Drone](http://localhost:8080): Drone is our CI/CD application, it will run the pipeline for all commit we push to the repo.

5. Happy bugfixing!

---

### Submit your test

After you are done with the test we need you to commit your container, log into docker and push your fixes to your docker-bub account.

Please execute the next 4 steps:

1. Commit the available container ( _**change the** `change-here-for-your-docker-hub-username` **for your docker-hub username**_ )

```bash
docker commit $(docker ps | grep mobile-test | awk '{print $1}') change-here-for-your-docker-hub-username/mobile-test
```

2. Log into docker-hub

```bash
docker login
```

3. Push your image ( _**change the** `change-here-for-your-docker-hub-username` **for your docker-hub username**_ )

```bash
docker push change-here-for-your-docker-hub-username/mobile-test
```

4. Send us back 
