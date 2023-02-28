# Blob store

ROAPI currently supports the following blob storages:

* Filesystem
* HTTP/HTTPS
* S3
* GCS
* Azure Storage

## Filesystem

Filesystem store can be specified using `file:` or `filesystem:` schemes.  In a
Windows environment, the scheme is mandatory.  On Unix systems, a uri without a
scheme prefix is treated as filesystem backed data source by ROAPI. 

For example, to serve a local parquet file `test_data/blogs.parquet`, you can
just set the uri to the file path:

```yaml
tables:
  - name: "blogs"
    uri: "test_data/blogs.parquet"
```

Filesystem store supports loading partitioned tables. In other words, you can
split up the table into mulitple files and load all of them into a single table
by setting uri to the directory path. When loading a partitioned dataset, you
will need to manually specify table format since the uri will not contain table
format as a suffix:

```yaml
tables:
  - name: "blogs"
    uri: "test_data/blogs/"
    option:
        format: "parquet"
```


## HTTP/HTTPS

ROAPI can build tables from datasets served through HTTP protocols. However, one
thing to keep in mind is HTTP store doesn't support partitioned datasets because
there is no native directory support in HTTP protocol.


## S3

ROAPI can build tables from datasets hosted in S3 buckets. Configuration is
similar to filesystem store:

```yaml
tables:
  - name: "TABLE_NAME"
    uri: "s3://BUCKET/TABLE/KEY"
    option:
        format: "csv"
```

Note that AWS region needs to be manually specified through `AWS_REGION`
environment variable.

To configure S3 credentials, you can use IAM role or set the following
environment variables if you are using IAM user:

* `AWS_SECRET_ACCESS_KEY`
* `AWS_ACCESS_KEY_ID`

## GCS

ROAPI can build tables from datasets hosted in GCS buckets. Configuration is
similar to filesystem store:

```yaml
tables:
  - name: "TABLE_NAME"
    uri: "gs://BUCKET/TABLE/KEY"
    option:
        format: "csv"
```

To configure GCS credentials, you can set the following
environment variables if you are using service accont:

* `GOOGLE_SERVICE_ACCOUNT` / `GOOGLE_SERVICE_ACCOUNT_PATH`: location of service account file
* `GOOGLE_SERVICE_ACCOUNT_KEY`: JSON serialized service account key
* `GOOGLE_APPLICATION_CREDENTIALS`: set by gcloud SDK
* [Google Compute Engine Service Account](https://cloud.google.com/compute/docs/access/service-accounts#associating_a_service_account_to_an_instance)
* [GKE Workload Identity](https://cloud.google.com/kubernetes-engine/docs/concepts/workload-identity)

## Azure Storage

ROAPI can build tables from datasets hosted in Azure Storage. Configuration is
similar to filesystem store:

```yaml
tables:
  - name: "TABLE_NAME"
    uri: "az://BUCKET/TABLE/KEY"
    option:
        format: "csv"
```

The supported url schemas are
* `abfs[s]://<container>/<path>`
* `az://<container>/<path>`
* `adl://<container>/<path>`
* `azure://<container>/<path>`

To configure Azure credentials, you can set the following
environment variables:

* `AZURE_STORAGE_ACCOUNT_NAME`
* `AZURE_STORAGE_ACCOUNT_KEY`
* `AZURE_STORAGE_CLIENT_ID`
* `AZURE_STORAGE_TENANT_ID`
* `AZURE_STORAGE_SAS_KEY`
* `AZURE_STORAGE_TOKEN`
* `AZURE_MSI_ENDPOINT` / `AZURE_IDENTITY_ENDPOINT`: Endpoint to request a imds managed identity token
* `AZURE_OBJECT_ID`: Object id for use with managed identity authentication
* `AZURE_MSI_RESOURCE_ID`: Msi resource id for use with managed identity authentication
* `AZURE_FEDERATED_TOKEN_FILE`: File containing token for Azure AD workload identity federation
