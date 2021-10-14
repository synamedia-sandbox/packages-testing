Created by Martin Lester 14 Oct 2021

This is a test of how we can use the packages area of GitHub.com to push docker containers and nmp etc

https://github.com/Synamedia-sandbox/packages-testing

Notes:
https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry#pushing-container-images

```
# docker build -t apline-echo .
# docker run apline-echo
WARNING: IPv4 forwarding is disabled. Networking will not work.
Hello Synamedia

```

https://github.com/settings/tokens/new?scopes=write:packages,delete:packages
Save the token somewhere

```
# export CR_PAT=<TOKEN>
# echo $CR_PAT | docker login ghcr.io -u <your useriid> --password-stdin

# docker tag apline-echo ghcr.io/synamedia-sandbox/alpine-echo
# docker push ghcr.io/synamedia-sandbox/alpine-echo
The push refers to repository [ghcr.io/synamedia-sandbox/alpine-echo]
e2eb06d8af82: Pushed
latest: digest: sha256:2a1f2b0f07538cc0ace66c4085d946cbcf9803bbb29786c10303cb70362b9fcd size: 528
```


