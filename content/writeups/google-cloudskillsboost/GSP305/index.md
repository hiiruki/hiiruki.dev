---
title: "[GSP305] Scale Out and Update a Containerized Application on a Kubernetes Cluster"
description: ""
summary: "Quest: Cloud Architecture: Design, Implement, and Manage"
date: 2023-05-25T07:55:03+07:00
draft: false
author: "Hiiruki" # ["Me", "You"] # multiple authors
tags: ["writeups", "challenge", "google-cloudskillsboost", "gsp305", "google-cloud", "cloudskillsboost", "juaragcp", "google-cloud-platform", "gcp", "container", "kubernetes", "cloud-computing", "cloud", "cloud-architecture"]
canonicalURL: ""
showToc: true
TocOpen: false
TocSide: 'right'  # or 'left'
weight: 5
# aliases: ["/first"]
hidemeta: false
comments: false
disableHLJS: true # to disable highlightjs
disableShare: true
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
# UseHugoToc: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
# editPost:
#     URL: "https://github.com/hiiruki/hiiruki.dev/blob/main/content/writeups/google-cloudskillsboost/GSP304/index.md"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

### GSP305

![Lab Banner](https://cdn.qwiklabs.com/GMOHykaqmlTHiqEeQXTySaMXYPHeIvaqa2qHEzw6Occ%3D#center)

- Time: 1 hour<br>
- Difficulty: Intermediate<br>
- Price: 5 Credits

Lab: [GSP305](https://www.cloudskillsboost.google/focuses/1739?parent=catalog)<br>
Quest: [Cloud Architecture: Design, Implement, and Manage](https://www.cloudskillsboost.google/quests/124)<br>

🔄 Last updated: Sep 7, 2023

## Challenge scenario

You are taking over ownership of a test environment and have been given an updated version of a containerized test application to deploy. Your systems' architecture team has started adopting a containerized microservice architecture. You are responsible for managing the containerized test web applications. You will first deploy the initial version of a test application, called `echo-app` to a Kubernetes cluster called `echo-cluster` in a deployment called `echo-web`.

Before you get started, open the navigation menu and select **Cloud Storage**. The last steps in the Deployment Manager script used to set up your environment creates a bucket.

Refresh the Storage browser until you see your bucket. You can move on once your Console resembles the following:

![bucket](./images/bucket.webp#center)

Check to make sure your GKE cluster has been created before continuing. Open the navigation menu and select **Kubernetes Engine** > **Clusters**.

Continue when you see a green checkmark next to `echo-cluster`:

![kubernetes cluster](./images/kubernetes_cluster.webp#center)

To deploy your first version of the application, run the following commands in Cloud Shell to get up and running:

```bash
gcloud container clusters get-credentials echo-cluster --zone=us-central1-a
```

```bash
kubectl create deployment echo-web --image=gcr.io/qwiklabs-resources/echo-app:v1
```

```bash
kubectl expose deployment echo-web --type=LoadBalancer --port 80 --target-port 8000
```

## Your challenge

You need to update the running `echo-app` application in the `echo-web` deployment from the v1 to the v2 code you have been provided. You must also scale out the application to 2 instances and confirm that they are all running.

1. Check that there is a tagged image in gcr.io for echo-app:v2.

    ```bash
    mkdir echo-web
    cd echo-web
    gsutil cp -r gs://$DEVSHELL_PROJECT_ID/echo-web-v2.tar.gz .
    tar -xzf echo-web-v2.tar.gz
    rm echo-web-v2.tar.gz
    docker build -t echo-app:v2 .
    docker tag echo-app:v2 gcr.io/$DEVSHELL_PROJECT_ID/echo-app:v2
    docker push gcr.io/$DEVSHELL_PROJECT_ID/echo-app:v2
    ```

2. Echo-app:v2 is running on the Kubernetes cluster.

    Deploy the first version of the application.

    ```bash
    gcloud container clusters get-credentials echo-cluster --zone=us-central1-a
    kubectl create deployment echo-web --image=gcr.io/qwiklabs-resources/echo-app:v1
    kubectl expose deployment echo-web --type=LoadBalancer --port 80 --target-port 8000
    ```

    Edit the `deployment.apps` file.

    ```bash
    kubectl edit deploy echo-web
    ```

    Start the editor by type `i`. Change `image=...:v1` to `image=...:v2`.

    `image=gcr.io/qwiklabs-resources/echo-app:v2`

    Save the `deployment.apps` file, hit **ESC** then type `:wq` and **Enter**.

3. The Kubernetes cluster deployment reports 2 replicas.

    ```bash
    kubectl scale deployment echo-web --replicas=2
    ```

4. The application must respond to web requests with V2.0.0.

    ```bash
    kubectl expose deployment echo-web --type=LoadBalancer --port 80 --target-port 8000

    kubectl get svc
    ```

## Congratulations!
