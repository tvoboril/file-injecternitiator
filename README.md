# file-injecternitiator
Inject a file from secrets into existing image

Replace env-notated strings with their variables

This simple image will use the `envsubst` command from the gettext package to replace all strings "annotated like variables" with the enviromentals passed into the container, or with existing variables injected by kubernetes etc.

This example will create new fortunes for the example node.js single page app: [O-Fortuna](https://github.com/jhunt/o-fortuna).

In use, a file is prepared and inserted into the o-fortuna pod with the `old-file.yaml` configMap.

The new variables are base64 encoded and inseted with `secrets.yaml`.

The init container in `deployment.yaml` ingests the configMap and the secrets and then uses envsubst to generate a new file.  That new file is shared with actual container through the use of an `emptyDir`.

The new file is then copied into place from the shared dir to the actual config location.

The docker image is built from: [Variable-Swap](https://github.com/tvoboril/variable-swap)
and can be found: [Docker Hub](https://hub.docker.com/repository/docker/tomvoboril/variable-swap).
It is available for multiple cpu architects.


`docker pull tomvoboril/variable-swap`



run with the following commands:


 `kubectl create fortuna`
 
 
 `kubectl apply -f .`
