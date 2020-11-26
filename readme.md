1. create cluster
2. connect to cluster
3. create service account 
    * https://cloud.google.com/anthos/gke/docs/aws/how-to/private-registry
    * `gcloud config set project gcp-pso-bfg-playground`
    * `gcloud iam service-accounts create kpack-sa`
    * `gcloud projects add-iam-policy-binding gcp-pso-bfg-playground \
         --member serviceAccount:kpack-sa@gcp-pso-bfg-playground.iam.gserviceaccount.com \
         --role roles/storage.admin`
    * `gcloud iam service-accounts keys create key.json \
         --iam-account kpack-sa@gcp-pso-bfg-playground.iam.gserviceaccount.com`
    * `kubectl create secret docker-registry gcr-secret \
               --docker-server=gcr.io \
               --docker-username=_json_key \
               --docker-email=kpack-sa@gcp-pso-bfg-playground.iam.gserviceaccount.com \
               --docker-password="$(cat key.json)"`
4. kpack tutorial
    * download release yaml and logs
    * https://github.com/pivotal/kpack/releases/download/v0.1.4/release-0.1.4.yaml
    * https://github.com/pivotal/kpack/blob/master/docs/tutorial.md
5. install kpack `kubectl apply -f kpack-release-0.1.4.yaml`
6. create k8s service account `kubectl apply -f kpack-sa.yaml`
7. create store`kubectl apply -f store.yaml`
8. create stack `kubectl apply -f stack.yaml`
9. create builder `kubectl apply -f builder.yaml`
10. create image `kubectl apply -f image.yaml`
11. use logs `./logs -image tutorial-image -namespace default`

 