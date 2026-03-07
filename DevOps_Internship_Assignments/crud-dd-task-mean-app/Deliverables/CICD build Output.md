Started by user Shriram Halyal
Obtained DevOps_Internship_Assignments/crud-dd-task-mean-app/crud-dd-task-mean-app/JenkinsFile from git https://github.com/shriramhalyal2000/Discover-Dollar-Apt/
[Pipeline] Start of Pipeline
[Pipeline] node
Running on Jenkins in /var/lib/jenkins/workspace/app-docker-deploy
[Pipeline] {
[Pipeline] stage
[Pipeline] { (Declarative: Checkout SCM)
[Pipeline] checkout
The recommended git tool is: NONE
No credentials specified
 > git rev-parse --resolve-git-dir /var/lib/jenkins/workspace/app-docker-deploy/.git # timeout=10
Fetching changes from the remote Git repository
 > git config remote.origin.url https://github.com/shriramhalyal2000/Discover-Dollar-Apt/ # timeout=10
Fetching upstream changes from https://github.com/shriramhalyal2000/Discover-Dollar-Apt/
 > git --version # timeout=10
 > git --version # 'git version 2.50.1'
 > git fetch --tags --force --progress -- https://github.com/shriramhalyal2000/Discover-Dollar-Apt/ +refs/heads/*:refs/remotes/origin/* # timeout=10
 > git rev-parse refs/remotes/origin/dev^{commit} # timeout=10
Checking out Revision 906fa81eb3dbf3392d3ed7a51b688e1a842f3575 (refs/remotes/origin/dev)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f 906fa81eb3dbf3392d3ed7a51b688e1a842f3575 # timeout=10
Commit message: "adding few changes"
 > git rev-list --no-walk b6c8c8fc9edee5d403a29ffeca5b80f45104488a # timeout=10
[Pipeline] }
[Pipeline] // stage
[Pipeline] withEnv
[Pipeline] {
[Pipeline] withEnv
[Pipeline] {
[Pipeline] stage
[Pipeline] { (Checkout)
[Pipeline] checkout
The recommended git tool is: NONE
No credentials specified
 > git rev-parse --resolve-git-dir /var/lib/jenkins/workspace/app-docker-deploy/.git # timeout=10
Fetching changes from the remote Git repository
 > git config remote.origin.url https://github.com/shriramhalyal2000/Discover-Dollar-Apt/ # timeout=10
Fetching upstream changes from https://github.com/shriramhalyal2000/Discover-Dollar-Apt/
 > git --version # timeout=10
 > git --version # 'git version 2.50.1'
 > git fetch --tags --force --progress -- https://github.com/shriramhalyal2000/Discover-Dollar-Apt/ +refs/heads/*:refs/remotes/origin/* # timeout=10
 > git rev-parse refs/remotes/origin/dev^{commit} # timeout=10
Checking out Revision 906fa81eb3dbf3392d3ed7a51b688e1a842f3575 (refs/remotes/origin/dev)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f 906fa81eb3dbf3392d3ed7a51b688e1a842f3575 # timeout=10
Commit message: "adding few changes"
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Build Docker Images)
[Pipeline] sh
+ echo 'Building Frontend...'
Building Frontend...
+ cd DevOps_Internship_Assignments/crud-dd-task-mean-app/crud-dd-task-mean-app/frontend
+ docker build -t shriram2105/mean-frontend:20 .
#0 building with "default" instance using docker driver

#1 [internal] load build definition from Dockerfile
#1 transferring dockerfile: 491B done
#1 DONE 0.0s

#2 [auth] library/node:pull token for registry-1.docker.io
#2 DONE 0.0s

#3 [internal] load metadata for docker.io/library/node:18-alpine
#3 DONE 0.1s

#4 [internal] load .dockerignore
#4 transferring context: 2B done
#4 DONE 0.0s

#5 [1/5] FROM docker.io/library/node:18-alpine@sha256:8d6421d663b4c28fd3ebc498332f249011d118945588d0a35cb9bc4b8ca09d9e
#5 DONE 0.0s

#6 [internal] load build context
#6 transferring context: 5.75kB done
#6 DONE 0.0s

#7 [2/5] WORKDIR /app
#7 CACHED

#8 [3/5] COPY package*.json ./
#8 CACHED

#9 [4/5] RUN npm install
#9 CACHED

#10 [5/5] COPY . .
#10 DONE 0.1s

#11 exporting to image
#11 exporting layers 0.0s done
#11 writing image sha256:06f1f174bb6dee88e3d26ca05d425f6e87705086c09e5599375436a012eadc87 done
#11 naming to docker.io/shriram2105/mean-frontend:20 done
#11 DONE 0.0s
+ echo 'Building Backend...'
Building Backend...
+ cd ../backend
+ docker build -t shriram2105/mean-backend:20 .
#0 building with "default" instance using docker driver

#1 [internal] load build definition from Dockerfile
#1 transferring dockerfile: 367B done
#1 DONE 0.0s

#2 [internal] load metadata for docker.io/library/node:18-alpine
#2 DONE 0.1s

#3 [internal] load .dockerignore
#3 transferring context:
#3 transferring context: 2B done
#3 DONE 0.0s

#4 [1/5] FROM docker.io/library/node:18-alpine@sha256:8d6421d663b4c28fd3ebc498332f249011d118945588d0a35cb9bc4b8ca09d9e
#4 DONE 0.0s

#5 [internal] load build context
#5 transferring context: 1.25kB done
#5 DONE 0.0s

#6 [2/5] WORKDIR /app
#6 CACHED

#7 [3/5] COPY package*.json ./
#7 CACHED

#8 [4/5] RUN npm install --only=production
#8 CACHED

#9 [5/5] COPY . .
#9 CACHED

#10 exporting to image
#10 exporting layers done
#10 writing image sha256:e7b9caacc63f3a56e88e52b99d6678c171fbda3d16be371682a54b99b4efbf71 done
#10 naming to docker.io/shriram2105/mean-backend:20 done
#10 DONE 0.0s
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Push Images to Docker Hub)
[Pipeline] withCredentials
Masking supported pattern matches of $DOCKER_PASS
[Pipeline] {
[Pipeline] sh
Warning: A secret was passed to "sh" using Groovy String interpolation, which is insecure.
		 Affected argument(s) used the following variable(s): [DOCKER_PASS]
		 See https://jenkins.io/redirect/groovy-string-interpolation for details.
+ echo ****
+ docker login -u shriram2105 --password-stdin
WARNING! Your password will be stored unencrypted in /var/lib/jenkins/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded
+ docker push shriram2105/mean-frontend:20
The push refers to repository [docker.io/shriram2105/mean-frontend]
2ca19fe1d6f8: Preparing
9af334c6447b: Preparing
9d41412828fb: Preparing
37b7466541cd: Preparing
82140d9a70a7: Preparing
f3b40b0cdb1c: Preparing
0b1f26057bd0: Preparing
08000c18d16d: Preparing
f3b40b0cdb1c: Waiting
0b1f26057bd0: Waiting
08000c18d16d: Waiting
9af334c6447b: Layer already exists
9d41412828fb: Layer already exists
37b7466541cd: Layer already exists
82140d9a70a7: Layer already exists
0b1f26057bd0: Layer already exists
f3b40b0cdb1c: Layer already exists
08000c18d16d: Layer already exists
2ca19fe1d6f8: Pushed
20: digest: sha256:04c583a597b94c53c8f730a97f22abe87bdf8c91ab714faa883fc82510a97016 size: 1995
+ docker push shriram2105/mean-backend:20
The push refers to repository [docker.io/shriram2105/mean-backend]
46676210c9bb: Preparing
736f42bc8fba: Preparing
bf23ab51edb6: Preparing
37b7466541cd: Preparing
82140d9a70a7: Preparing
f3b40b0cdb1c: Preparing
0b1f26057bd0: Preparing
08000c18d16d: Preparing
f3b40b0cdb1c: Waiting
0b1f26057bd0: Waiting
08000c18d16d: Waiting
736f42bc8fba: Layer already exists
82140d9a70a7: Layer already exists
46676210c9bb: Layer already exists
37b7466541cd: Layer already exists
bf23ab51edb6: Layer already exists
f3b40b0cdb1c: Layer already exists
0b1f26057bd0: Layer already exists
08000c18d16d: Layer already exists
20: digest: sha256:b91dd596de543227eaaa4b12f685fba2b77d3dea27747cfff7e6177d79417603 size: 1991
+ docker tag shriram2105/mean-frontend:20 shriram2105/mean-frontend:latest
+ docker push shriram2105/mean-frontend:latest
The push refers to repository [docker.io/shriram2105/mean-frontend]
2ca19fe1d6f8: Preparing
9af334c6447b: Preparing
9d41412828fb: Preparing
37b7466541cd: Preparing
82140d9a70a7: Preparing
f3b40b0cdb1c: Preparing
0b1f26057bd0: Preparing
08000c18d16d: Preparing
f3b40b0cdb1c: Waiting
0b1f26057bd0: Waiting
08000c18d16d: Waiting
2ca19fe1d6f8: Layer already exists
82140d9a70a7: Layer already exists
9d41412828fb: Layer already exists
37b7466541cd: Layer already exists
9af334c6447b: Layer already exists
0b1f26057bd0: Layer already exists
f3b40b0cdb1c: Layer already exists
08000c18d16d: Layer already exists
latest: digest: sha256:04c583a597b94c53c8f730a97f22abe87bdf8c91ab714faa883fc82510a97016 size: 1995
+ docker tag shriram2105/mean-backend:20 shriram2105/mean-backend:latest
+ docker push shriram2105/mean-backend:latest
The push refers to repository [docker.io/shriram2105/mean-backend]
46676210c9bb: Preparing
736f42bc8fba: Preparing
bf23ab51edb6: Preparing
37b7466541cd: Preparing
82140d9a70a7: Preparing
f3b40b0cdb1c: Preparing
0b1f26057bd0: Preparing
08000c18d16d: Preparing
f3b40b0cdb1c: Waiting
0b1f26057bd0: Waiting
08000c18d16d: Waiting
37b7466541cd: Layer already exists
bf23ab51edb6: Layer already exists
82140d9a70a7: Layer already exists
736f42bc8fba: Layer already exists
46676210c9bb: Layer already exists
0b1f26057bd0: Layer already exists
f3b40b0cdb1c: Layer already exists
08000c18d16d: Layer already exists
latest: digest: sha256:b91dd596de543227eaaa4b12f685fba2b77d3dea27747cfff7e6177d79417603 size: 1991
[Pipeline] }
[Pipeline] // withCredentials
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Deploy to EC2)
[Pipeline] sshagent
[ssh-agent] Using credentials ec2-user (ec2-ssh-key)
$ ssh-agent
SSH_AUTH_SOCK=/tmp/ssh-XXXXXXsaY0xh/agent.23658
SSH_AGENT_PID=23661
Running ssh-add (command line suppressed)
Identity added: /var/lib/jenkins/workspace/app-docker-deploy@tmp/private_key_13245898560093345716.key (/var/lib/jenkins/workspace/app-docker-deploy@tmp/private_key_13245898560093345716.key)
[ssh-agent] Started.
[Pipeline] {
[Pipeline] sh
+ ssh -o StrictHostKeyChecking=no ec2-user@ec2-54-236-201-80.compute-1.amazonaws.com '
                          set -e
                          echo "Pulling Latest Images..."
                          docker pull shriram2105/mean-frontend:20
                          docker pull shriram2105/mean-backend:20

                          export TAG=20
                          cd /home/ec2-user
                          docker-compose down || true
                          docker-compose up -d --force-recreate

                          echo "Deployment done successfully 🎯"
                        '
Pulling Latest Images...
20: Pulling from shriram2105/mean-frontend
Digest: sha256:04c583a597b94c53c8f730a97f22abe87bdf8c91ab714faa883fc82510a97016
Status: Image is up to date for shriram2105/mean-frontend:20
docker.io/shriram2105/mean-frontend:20
20: Pulling from shriram2105/mean-backend
Digest: sha256:b91dd596de543227eaaa4b12f685fba2b77d3dea27747cfff7e6177d79417603
Status: Image is up to date for shriram2105/mean-backend:20
docker.io/shriram2105/mean-backend:20
time="2025-11-28T10:58:08Z" level=warning msg="/home/ec2-user/docker-compose.yaml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion"
 Container frontend  Stopping
 Container frontend  Stopped
 Container frontend  Removing
 Container frontend  Removed
 Container backend  Stopping
 Container backend  Stopped
 Container backend  Removing
 Container backend  Removed
 Container mongo  Stopping
 Container mongo  Stopped
 Container mongo  Removing
 Container mongo  Removed
 Network ec2-user_app-network  Removing
 Network ec2-user_app-network  Removed
time="2025-11-28T10:58:11Z" level=warning msg="/home/ec2-user/docker-compose.yaml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion"
 Network ec2-user_app-network  Creating
 Network ec2-user_app-network  Created
 Container mongo  Creating
 Container mongo  Created
 Container backend  Creating
 Container backend  Created
 Container frontend  Creating
 Container frontend  Created
 Container mongo  Starting
 Container mongo  Started
 Container backend  Starting
 Container backend  Started
 Container frontend  Starting
 Container frontend  Started
Deployment done successfully 🎯
[Pipeline] }
$ ssh-agent -k
unset SSH_AUTH_SOCK;
unset SSH_AGENT_PID;
echo Agent pid 23661 killed;
[ssh-agent] Stopped.
[Pipeline] // sshagent
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Declarative: Post Actions)
[Pipeline] echo
Build finished with status: SUCCESS
[Pipeline] }
[Pipeline] // stage
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // node
[Pipeline] End of Pipeline
Finished: SUCCESS