# CipherCompute

Start and try Cosmian CipherCompute easily just by using Docker Compose

```console
sudo docker-compose up
```

A full local environment is provided to help you run collaborative computations, including user interface.

## Quickstart

Let's say we want to find common IDs between 2 CSV datasets:
- [dataset participant 0](data/participant_0/data.csv)
- [dataset participant 1](data/participant_1/data.csv)

These 2 datasets are owned by two companies and are very sensitive, so they cannot be shared in cleartext to each other participants.

This MPC (Multi-Party Computation) program has been designed in Rust to compute a merge join and will be used in this example.

The MPC system requires 3 participants at minimum, so in this example one participant will play the role of an arbiter.

Steps:
- start 3 different browsers (see known issues) and connect the UIs (login: `hello@world.com` / pwd: `azerty`):
  - participant 0 - http://localhost:3000
  - participant 1 - http://localhost:3001
  - participant 2 - http://localhost:3002
- go to participant 0 UI
- create a new computation using the wizard and specify required datasource (take a look at mentioned CSV datasets)
- specify the MPC code that will be run (i.e.: [mpc_join_2_participants](https://github.com/Cosmian/mpc_join_2_participants.git)) to perform this merge join operation
- specify which data from the dataset will be used (i.e.: which column of your CSV file)
- go to participant 1 UI, specify the datasource that will be used and then approve pending computation
- go to participant 2 UI and approve pending computation
- go back to participant 0 UI, do a final review and run the computation
- check the results

## Create your own MPC program written in Rust

[Try our MPC code template generator](https://github.com/Cosmian/mpc_rust_template)

## Known issues

Security issues:
- UI is running without HTTPs
- communication between orchestrators are NOT encrypted at the moment and are performed directly from orchestrators to orchestrators

Others:
- cookies are shared among browser, using the same browser for the 3 UIs will make you re-login each time you jump from one UI to another. Normally the 3 UIs are used from different people. To solve this, please use different browsers (i.e.: firefox, firefox incognito mode, brave)
