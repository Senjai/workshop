# Laptop Setup - Ruby Microservices Workshop

## Software Prerequisites

- Ruby (minimum version: 2.4)
- Postgres (minimum version: 9.5)
- Git (minimum version: 2)
- GCC (already included with Apple XCode Developer Tools)

## Setup

### Start Postgres

If you've installed Postgres through Homebrew on Mac:

```
launchctl load -w ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist
```

If you don't want to start it as a daemon, open a new terminal window and run:

```
postgres -D /usr/local/var/postgres
```

Note that closing the terminal window will cause the database to shut down. If you've started the database with `Postgres -D`, keep the terminal window open for as long as you need to use the database.

On nix:

```
sudo systemctl start postgresql
```

#### Note for Linux Users

Postgres installations on Linux can vary between OS distributions as well as the package manager used.

When Postgres is installed on a Linux machine, it is often configured by default for security considerations that reflect server operations. Make sure that you are aware of the runtime requirements of Postgres on your environment if you are running Linux.

In particular, many Postgres setups on Linux require passwords for all database connections over TCP. This will either need to be disabled, or passwords will have to be configured for the role used during the workshop exercises.

If your system is setup for peer authentication, you will have to remove the password, host, and port keys from the json configuration below. The table would have been created under your system user account instead of event_source.

### Clone this Repository

This is the repository that we'll be working with through the course the workshop.

Clone the workshop repository to your machine:

```
git clone git@github.com:eventide-tutorial/workshop.git
```

Or, if you prefer to retrieve the repository over SSH:

```
git clone https://github.com/eventide-tutorial/workshop.git
```

### Change Directory to the Workshop Directory

```
cd workshop
```

## Test the Setup

### Change Directory to the Setup Verification Directory

```
cd verify_setup
```

### Install the Gems

```
./install_gems.sh
```

### Create the Database

A database named `event_source` along with a user of the same name will be created.

Run:

```
bundle exec evt-pg-recreate-db
```

### Copy the Database Settings Example File

```
cp settings/event_source_postgres.json.example settings/event_source_postgres.json
```

### Set the Database Password (Optional)

If your database installation requires a password (see _Note for Linux Users_ above), edit `settings/event_source_postgres.json` and change the password value to the database's password.

### Run the Test

```
./test.sh
```

If everything is working correctly, you should see the following output:

```
Running /Users/sbellware/projects/eventide/tutorial/account-component-skeleton/test/automated/database_connection.rb
Database Connection
  Connects on first use

Finished running 1 file
Ran 1 test in 0.052s (19.264s tests/second)
1 passed, 0 skipped, 0 failed, 0 total errors
```

### Get the Example Project Code

```
./get_account_code.sh
```
