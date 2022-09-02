## Publish a Docker image to Google Cloud Registry

1. Prepare your GCP client for Spark inside the workspace

```
cd /mnt/code

. publish_to_gcp_cloud_build.sh
```

This is an environment for a workspace so remember to add the `Pluggable Workspace Tools` section

2. Create a Service Account on GCP
- Create service account on GCP
- Generate keys for this service account
- Download the keys as a json file. Name it `keys.json`

3. Create a Domino project using this repo and start a workspace using the environment we built in step 1

4. Upload the file `keys.json` in `/tmp/` folder of the workspace

5. Ensure that you set the following project (Set them as user specific environment variables)
```shell
export GCP_PROJECT_ID=${GCP_PROJECT_ID:-unknown}
export SERVICE_ACCOUNT_NAME=${SERVICE_ACCOUNT_NAME:-unknown}
```

6. Finally execute the command
   `./publish_to_gcp_cloud_build.sh example-model`
   
7. If this succeeds go to the `Cloud Run` service in GCP and deploy the image above as a Google Cloud Service

8. Test the endpoint

```shell
curl --location --request POST 'https://<service_endpoint>/predict' \
--header 'Content-Type: application/json' \
--data-raw '{"data": {"start": 1, "stop": 100}}'
```

9. You can also deploy the file `model.py` and the `predict` function to Model API



## Run a Spark Job which integrates with Google Cloud Storage

Run the workbook GCS_WK.ipynb