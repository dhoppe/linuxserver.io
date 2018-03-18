---
path: "/docs/executing-containers"
date: "2018-03-18"
title: "Executing and Inspecting"
---

<div class="preface">
A useful tool to determine application and build versions, as well as debugging.
</div>

## Shell Access

Particularly useful when debugging the application - to shell in to one of our containers, run the following:

```bash
docker exec -it <container_name> /bin/bash
```

## Tailing the logs

The vast majority of our images are configured to output the application logs to the console, which in Docker's terms means you can access them using the `docker logs` command:

```bash
docker logs -f --tail=<number_of_lines_to_start_with> <container_name>
```

The `--tail` argument is optional, but useful if the application has been running for a long time - the `logs` command by default will output _all_ logs.

## Checking the build version

If you are experiencing issues with one of our containers, it helps us to know which version of the image your container is running from. The primary reason we ask for this is because you may be reporting an issue we are aware of and have subsequently fixed. However, if you are running on the latest version of our image, it could indeed be a newly found bug, which we'd want to know more about.

To obtain the build version for the image:

```bash
docker inspect -f '{{ index .Config.Labels "build_version" }}' <container_name>
```

Or the container:

```bash
docker inspect -f '{{ index .Config.Labels "build_version" }}' linuxserver/<image_name>
```