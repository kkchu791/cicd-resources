# Understanding Github Actions

automate all software engineer workflow

CI/CD (continuous integrations/ continuous deployment)

Trigger workflow w/ an event like a merge

runner - the machine (or enviornment) that executes a job's steps
 - each job gets a fresh Virtual Machine (VM)
 - in this VM -> you can run the job's commands (build test deploy)
 - after it gets thrown away
 - isolation means jobs can't interfere w/ each other or leave state behind

workflow file - describes what to do
runner - worker that does it

![[Pasted image 20261016162735.png]]

`steps:
	- users: actions/checkout@v4 // action - package someone else wrote
	- run: npm test // script - terminal commands, uses run

multiple runners can work on one workflow file:
one runner per job,
workflow can have many jobs

jobs1(build): run tests, build docker image, push to ECR
jobs2(deploy): update the ECS services to use the new image

jobs:
	build:
		runs-on: ubuntu-latest
		 steps: [...] #test, docker build, push to ECR\
	 deploy:
		 needs: build
		 runs-on: ubuntu-latest
		 steps: [...] #update ecs

without needs, jobs run in parallel on separate runners

Each job will run inside its own VM runner,

**workflows:** 
	a process your customize to run one or more jobs.
	 will run by an event or triggered manually

You can reference a workflow within another workflow

**events:**
an event triggers a workflow run.

**jobs:**
is a set of steps in a workflow that is executed on the same runner.

each step is a shell script or action

since each step is executed on the same runner, you can share dataf rom one step to another

steps run in order but can run in parralllel
can also use matrix to run the same job multiple times, each w/ a different combo of variables

**actions:**
reusable predefined packages to make your life easier

**runners**:
a server that runs your workflows when they're triggered
they can run only a single job a a time
github provides Linux and MacOS runner to run your workflows

Each workflow runs in a fresh newly provisioned VM.

