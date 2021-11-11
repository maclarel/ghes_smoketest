# GHES Smoke Test

This is a Python script that will hit various API endpoints (in moderate volumes) using a provided PAT and report on success/failure rates.  The tool will clean up after itself, deleting any repositories/issues/files/etc... created during testing.

This tool will specifically test functionality using _newly created repositories_. It is not intended to advise on the health of any existing repositories, and should not be used as the only source of truth for validating functionality of GitHub Enterprise Server.

## Requirements

- Python 3
- `requests` module (`$ python -m pip install requests`)
- Supplied PAT must have `delete_repo, repo` scopes

## Usage

```
python3 smoketest.py [-p] -pat PERSONAL_ACCESS_TOKEN [-t] -target GHES_URL [-debug]

Performs simple testing against GitHub Enterprise Server to ensure basic functionality. By default, each endpoint will be tested 10 times.

Required arguments:
    -p, -pat    The personal access token to use for access
    -t, -target   The URL of the target GitHub Enterprise Server instance (e.g. https://github.company.com)

Optional arguments:
    -debug      Display response output as JSON
```

## Example output

```
$ python3 smoketest.py -p <pat_for_user1_goes_here> -t https://github.fakecompany.net
2021-11-11 12:17:14,902 INFO: Server at https://github.fakecompany.net/status appears to be up!
2021-11-11 12:17:15,074 INFO: Running as user1 - PAT auth confirmed working
2021-11-11 12:17:15,074 INFO: Testing creation of smoketest repositories
2021-11-11 12:17:22,845 INFO: Repostiory creation returned 0 errors
2021-11-11 12:17:22,845 INFO: Testing creation of Issues in smoketest repositories
2021-11-11 12:17:28,285 INFO: Issue creation returned 0 errors
2021-11-11 12:17:28,285 INFO: Testing file creation in each smoketest repository
2021-11-11 12:17:34,250 INFO: File creation returned 0 errors
2021-11-11 12:17:34,250 INFO: Testing deletion of smoketest repositories
2021-11-11 12:17:37,979 INFO: Repository deletion returned 0 errors
```
