# QueueCTL-backend
QueueCTL is a CLI-based job queue system with persistent storage, multiple workers, automatic retries with exponential backoff, and a Dead Letter Queue. It allows enqueuing, managing, and monitoring background jobs efficiently via simple CLI commands.
#Tech Stack

Node.js (v22+ recommended)
SQLite via better-sqlite3
CLI management via commander
UUID generation via uuid

#Setup Instructions
Clone the repository:
git clone https://github.com/SaiChandanaSriYelay/QueueCTL-backend.git
cd queuectl


Install dependencies:
npm install

#CLI Usage Examples
Enqueue a Job
node queuectl.js enqueue '{"id":"job1","command":"echo Hello World"}'


Output:

Job enqueued successfully: job1

List Jobs by State
node queuectl.js list --state pending
Run Worker(s)
node queuectl.js worker --count 1
List DLQ Jobs:

node queuectl.js dlq:list
Purge DLQ:

node queuectl.js dlq:purge

Architecture Overview

CLI Layer (queuectl.js): Handles all commands (enqueue, list, worker, DLQ, config, summary)

Job Management (jobManager.js): Job enqueueing, state updates, DLQ handling, and queue summary

DLQ Management (dlqManager.js): Retry and list DLQ jobs

Worker (worker.js): Continuously polls pending jobs, executes them, retries failures

Database Layer (db.js): Initializes SQLite tables (jobs, config, dlq)

Testing Instructions

Run the minimal test script:

node testQueuectl.js


Enqueues a job

Lists pending jobs

Runs a worker to execute jobs

Shows completed, failed, and DLQ jobs

Purges DLQ


Features

Enqueue and manage background jobs via CLI

Multiple worker support

Retry mechanism with exponential backoff

Dead Letter Queue (DLQ) for failed jobs

Persistent SQLite database storage

Clean CLI interface

Minimal testing script included

⚖️ Assumptions & Trade-offs

Uses SQLite for simplicity; scalable DB (MySQL/Postgres) can be added later.

CLI-only interface; no web UI implemented.

Job commands executed using exec; long-running jobs may require enhancements.

Exponential backoff uses a simple retry counter; jitter/randomization can be added later.
