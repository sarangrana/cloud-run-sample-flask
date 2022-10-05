Testing Cloud Build
# cloud-run-sample-flask

## 1. Introduction

This project is a simple Flask app developed for helping to illustrate how to set up a deployment pipeline on GCP with Cloud Builder, Container Registry and Cloud Run.

Check the complete tutorial [here](https://medium.com/ci-t/how-to-set-up-a-deployment-pipeline-on-gcp-with-cloud-build-container-registry-and-cloud-run-73391f5b77e4).

## 2. Environment setup

### 2.1. Get the code

```bash
git clone git@github.com:ivamluz/cloud-run-sample-flask.git
cd cloud-run-sample-flask
```

### 2.2. Virtualenv

- Install Python 3.7+

- Create and activate an isolated Python environment

  ```bash
  virtualenv venv
  source ./venv/bin/activate
  ```

- Install the dependencies

  ```bash
  pip install --upgrade -r requirements.txt
  ```

## 3. Run the app locally

```bash
cd app

HASHED_API_KEY=`../scripts/hash_value.py --value "1234"` \
  gunicorn --bind :8080 --workers 1 --threads 8 app:app --reload
```

Here, `HASHED_API_KEY` is a variable used by the application to set up a basic auth mechanism. The intent of this is to show how to configure and use environment variables on Google Cloud Run.

## 4. Testing the app

From a different terminal instance, run the following command (notice the value for the `x-api-key` is the unhashed value passed to the `HASHED_API_KEY` variable in the previous command):

```bash
curl \
  -H'x-api-key: 1234' \
  'http://localhost:8080/hello'
```

**Expected Output**

```console
{"hello":"world"}
```

If you see the output above, it means everything is working as expected.

After everything is running, please make sure to keep reading the [tutorial](https://medium.com/ci-t/how-to-set-up-a-deployment-pipeline-on-gcp-with-cloud-build-container-registry-and-cloud-run-73391f5b77e4).

## 5. Branching Strategy

Master Branch : Main branch of the source code repo, super stable. Only allowed to be merged from develop or hotfix.

Develop Branch : The main source branch for any of the feature branch creation, allowed to be merged from any feature branch after successful test case pass and via raising a pull request.

Feature Branch : This is a branch which should be created from Develop whenever any new feature needs to be implemented, once the work is completed it should be merged back  to develop via raising a pull request once all the test cases are approved.

![image](https://user-images.githubusercontent.com/36162846/194178703-c3636b06-bae1-4e63-85f1-a9f949c4ae35.png)

