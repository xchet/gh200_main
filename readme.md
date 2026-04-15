# GH-200 -GitHub Actions
## Automate your workflows with GitHub Actions

# Requirements to join the training

## Software development - basic
Enterprise Dev Knowledge - General awareness of CI/CD pipelines

GitHub familiarity

IDE and collaborations tools

# Trainer information
Name: Chinechetam Okafor (Chetam)
M365 Solution architect and Cloud consultant
LinkedIn: ../chetamokafor


# Introduction to GitHub Actions
What is GitHub Actions?

GitHub Actions is a CI/CD and workflow automation platform built directly into GutHub.
- It lets you to automate software workflows, testing, building, deploying
- in response to an event that happens inside your repo.

Key Concepts
1. CI/CD
    - Continuous Integration (CI): is the practice of auto testing every code changes.
    - Continuous Delivery/Deployment (CD): automatically delivers tested codes to production or staging environment

2. Why Actions over external tools?
    - Actions is natively integrated with GitHub: It reads your repo, respects your permissions model, and required no separate account or webhook plumbing.

# Core Concepts

The core concept is th three nested units that form the backbone of every automation.

A workflow contains jobs: each job contains steps.
1. Workflows - A YAML file in `.github/workflows/` - this definewhen automation runs and what it does. One repo can have many workflow2.

2. Jobs - A group of steps that run on the same virtual machine (runner) - Jobs runs in parallel by default unless you specify dependencies.

3. Step - An individual command or action inside a job. Steps run sequentially and share the same filesystem with in the job.

Workflow
    - Job1
        step1
        step2
        step3
    - Job2
        step1
        step2
        step3
    ...

-  `git push origin main` - push - trigger the workflow to run

on: push

# Events and Triggers

Events are the `why did this run?` of the workflow. GitHub fire an event when something happens in the repo - a push, a PR, a scheduled cron, or even a manuall button click

## Key Concepts
### `push` / `pull_requests`
Most common triggers, `push` fire when commits lands on a branch: `pull_request`  fires when a PR is opened, synched, or updated.

### `schedule`
A cron expression that fires the workflow on a time, independent of code activity - Useful for nightly buily build or stale-issue cleanup.

### `workflow_dispatch`
Enables a manual 'Run Workflow' button in the GitHub UI. - they optionally accept params

# Runners
A runner is the virtual or physicl machine that executes a job. Github provides hosted runners: you can also host your own for custom hardwares needs.

1. GitHub-hosted runners -Managed Ubuntu, Windows, and macOS VM. Eche job get a fresh ephemeral runner with a pre-installed software suite.

2. Selfhosted runners - Your own machine registered with GitHub.


# Module 2 - Writing your first workflow
Translate theory into practice.

## Workflow file anatomy (YAML Syntax)

A workflow file is a valid YAML placed in `.github/workflows/`. 
name, on, env, and jobs
Indentation is significant - use 2 space, not tabs

Key Concept
1. name key - optional label shown in the GitHub actions tab
2. on key - defines the trigger
3. jobs key - set of steps

# Automating CI - Build and Test

## Setting up a build matrix
Node.js v18, 20, 25
### `strategy.matrix`
- an object under the job definition that defines variable axes.

- `${{ matrix.variable }}`
Expression syntax to refernce a matrix variable in your step commands - eg, node-version `${{matrix.node}}`

    `strategy:`
        `matrix:`
            `node-version: ${{matrix.node}}`

## Caching dependencies
actions/cache
cache key - A harsh-based string indentifying a specific cache. typically includes the OS and a hash of your lock file
restore-keys

Setup cache key using hashFiles
use key: ${{runner.os}}-node-${{hashFiles('**/package-lock.json')}}

## Running Tests and uploading results

