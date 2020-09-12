# Kubernetes Dashboard

* GitHub repo: https://github.com/kubernetes/dashboard.
* Apply *dashboard.yaml*. You can get a newer version from [here](https://github.com/kubernetes/dashboard/blob/master/aio/deploy/recommended.yaml).
* Retrieve user token with:
    ```bash
    $ kubectl -n kubernetes-dashboard describe secret kubernetes-dashboard |grep ^token 
    ```
* Start kubernetes proxy with:
    ```bash
    $ kubectl proxy
    ```
* Apply *dashboard-admin.yaml* in order to grant admin access to the dashboard user (this is a really bad idea, unless for testing purposes).
* Access with the token retrieved to:
    ```
    http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/
    ```

**Note:** You may want to tune the user [access control](https://github.com/kubernetes/dashboard/blob/master/docs/user/access-control/README.md) in order to grant access to the dashboard to the resources.