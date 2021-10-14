Created by Martin Lester 14 Oct 2021

This is a test of how we can use the packages area of GitHub.com to push docker containers and nmp etc

https://github.com/Synamedia-sandbox/packages-testing

Notes:

https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry#pushing-container-images

Create the Docker image

```
# docker build -t apline-echo .
# docker run apline-echo
WARNING: IPv4 forwarding is disabled. Networking will not work.
Hello Synamedia

```

Create a PAT to use for managing packages

https://github.com/settings/tokens/new?scopes=write:packages,delete:packages

Save the token somewhere
Authorise the token for use with the Org
Push the container

```
# export CR_PAT=<TOKEN>
# echo $CR_PAT | docker login ghcr.io -u <your useriid> --password-stdin

# docker tag apline-echo ghcr.io/synamedia-sandbox/alpine-echo
# docker push ghcr.io/synamedia-sandbox/alpine-echo
The push refers to repository [ghcr.io/synamedia-sandbox/alpine-echo]
e2eb06d8af82: Pushed
latest: digest: sha256:2a1f2b0f07538cc0ace66c4085d946cbcf9803bbb29786c10303cb70362b9fcd size: 528
```

Link the package to a repo:
- goto the org
- click the packages tab
- select the package
- Goto the package settings
- Select link to repo
- Select the repo from the list

Test we can pull the image from the GH packages repository
First clean up

```
# docker rmi -f apline-echo ghcr.io/synamedia-sandbox/alpine-echo
# docker logout
# docker pull ghcr.io/synamedia-sandbox/alpine-echo:latest
Error response from daemon: Get https://ghcr.io/v2/synamedia-sandbox/alpine-echo/manifests/latest: unauthorized
```

Login and pull the image

```
# echo $CR_PAT | docker login ghcr.io -u <your useriid> --password-stdin
# docker pull ghcr.io/synamedia-sandbox/alpine-echo:latest
latest: Pulling from synamedia-sandbox/alpine-echo
a0d0a0d46f8b: Already exists
Digest: sha256:2a1f2b0f07538cc0ace66c4085d946cbcf9803bbb29786c10303cb70362b9fcd
Status: Downloaded newer image for ghcr.io/synamedia-sandbox/alpine-echo:latest
ghcr.io/synamedia-sandbox/alpine-echo:latest
# docker run --rm ghcr.io/synamedia-sandbox/alpine-echo:latest
WARNING: IPv4 forwarding is disabled. Networking will not work.
Hello Synamedia
```
