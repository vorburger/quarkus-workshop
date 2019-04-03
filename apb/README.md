# Setting up a Che environment with Quarkus stack

## Minishift preparation

    minishift profile set quarkus-workshop
    minishift addon enable admin-user
    minishift config set memory 8192
    minishift config set cpus 3
    minishift start

## OpenShift

If running via your own machine you can run the following command:

    oc login -u system:admin

Test if `oc whoami -t` successfully prints a token.  If it prints an error on Minishift, use `oc login -u admin` instead.

Then continue as follows:

    oc new-project labs-infra

    oc run apb --restart=Never --image="quay.io/tqvarnst/quarkus-workshop-apb" \
               --image-pull-policy="Always" \
               -- provision -vvv \
               -e namespace="$(oc project -q)"  \
               -e openshift_token=$(oc whoami -t) \
               -e che_generate_user_count=10

If you are using Minishift locally, you may want to use only `che_generate_user_count=1` (instead of `10`).

then follow the logs:

    oc logs apb -f

To start over from scratch, the easiest is to delete the project and re-create a new one before running the APB again:

    oc delete project labs-infra
    oc new-project labs-infra
    oc run apb ...
