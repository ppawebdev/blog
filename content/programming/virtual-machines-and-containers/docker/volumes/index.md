---
authors: [ "Geoffrey Hunter" ]
categories: [ "Programming", "Virtual Machines And Containers", "Docker" ]
date: 2017-05-23
draft: false
tags: [ "Docker", "volumes", "Dockerfile" ]
title: Volumes
type: page
---

<h2>Overview</h2>

<p>Volumes is a docker concept which allows you to have persistent storage within a docker container. It also allows files to be shared between the docker container and the host machine.</p>

<h2>Creating A Docker Volume</h2>

<p>A Docker volume can be associated with a host directory. This is specified as part of the <code>-v</code> option. Unlike the container path, which must be absolute, the host directory can be relative.</p>

<p>The following command will mount the relative host directory <code>my-volume/</code> to <code>/root/</code> inside the container.</p>

{{< highlight bash >}}
$ docker run -it -v my-volume:/root container
{{< /highlight >}}

{{% note %}}
Any existing files in <code>/root/</code> will be shadowed by this mount. This means that you cannot expose pre-existing files that reside in the container to the root system using this method.
{{% /note %}}

## Using A Dockerfile

Be careful with your placement of the `VOLUME` command inside a Dockerfile, as it essentially creates an immutable folder structure from that point forwards. Any modifications to the mount directory (or any sub-directory) will not be present when you create a container from the built image.