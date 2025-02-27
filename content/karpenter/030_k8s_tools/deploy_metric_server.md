---
title: "Deploy the Metric server"
date: 2020-03-07T08:30:11-07:00
weight: 20
---

## Deploy the Metrics Server

Metrics Server is a scalable, efficient source of container resource metrics for Kubernetes built-in autoscaling pipelines. These metrics will drive the scaling behavior of the [deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/). We will deploy the metrics server using [Kubernetes Metrics Server](https://github.com/kubernetes-sigs/metrics-server).

```sh
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/download/v0.6.0/components.yaml
```

Lets' verify the status of the metrics-server `APIService` 

```sh
kubectl get apiservice v1beta1.metrics.k8s.io -o json | jq '.status'
```

{{% notice note %}}
It may take a minute or so for the metric service to fully initialize. If on your first attempt you don't get the output indicated below, wait for a minute or so and try again.
{{% /notice %}}

If all is well, you should see a status message similar to the one below in the response

```json
{
  "conditions": [
    {
      "lastTransitionTime": "2021-12-01T19:22:27Z",
      "message": "all checks passed",
      "reason": "Passed",
      "status": "True",
      "type": "Available"
    }
  ]
}
```
