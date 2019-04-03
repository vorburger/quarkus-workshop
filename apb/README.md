# Setting up a the Vert.x 

If running via your own machine you can run the following command

  ```
  oc login -u system:admin

  oc new-project labs-infra

  oc run apb --restart=Never --image="quay.io/tqvarnst/quarkus-workshop-apb" \
             --image-pull-policy="Always" \
             -- provision -vvv \
             -e namespace="$(oc project -q)"  \
             -e openshift_token=$(oc whoami -t) \
             -e che_generate_user_count=10
  ```

to follow the logs
  ```
  oc logs apb -f
  ```
