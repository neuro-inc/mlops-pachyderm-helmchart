# Pachyderm Helm Chart README is [here](README-pachy.md)

# Deploy with MINIO
1. Create MinIO bucket and store following access info:
    - MINIO_ENDPOINT=minio.minio:9000
    - MINIO_BUCKET=pachyderm
    - MINIO_ACCESS_KEY=2B9GO0W97...
    - MINIO_SECRET_KEY=IXO-KZcus6uXd...

2. Clone this repo, chekout branch if needed
    ```shell
    $ git clone https://github.com/neuro-inc/mlops-pachyderm-helmchart/ && cd mlops-pachyderm-helmchart
    ```

3. Deploy:
    ```shell
    $ helm -n pachyderm upgrade pachyderm ./pachyderm -i --create-namespace --wait --timeout 600s \
        -f ./pachyderm/values.yaml \
        --set pachd.storage.backend=MINIO \
        --set pachd.storage.minio.bucket=$MINIO_BUCKET \
        --set pachd.storage.minio.endpoint=$MINIO_ENDPOINT \
        --set pachd.storage.minio.id=$MINIO_ACCESS_KEY \
        --set pachd.storage.minio.secret=$MINIO_SECRET_KEY \
        --set pachd.service.type=LoadBalancer
    ```
