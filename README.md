# Docker Images for dictyBase

<!--[![Build Status](https://travis-ci.org/docker-library/official-images.svg?branch=master)](https://travis-ci.org/docker-library/official-images)-->
Repository for managing docker images that will be used to deploy software
developed at [dictybase](https://github.com/dictyBase). The process will mostly
follow the guidelines and principles of the
[official](https://github.com/docker-library/official-images) repository.
So, be sure to familiarize yourself with the [Guidelines for Creating and
Documenting Official
Repositories](https://docs.docker.com/docker-hub/official_repos/) and the [Best
practices for writing
Dockerfiles](https://docs.docker.com/articles/dockerfile_best-practices/) in the
Docker documentation.

Also, the documentation for these images is currently stored separately in the
[dictybase-docker/docs](https://github.com/dictybase-docker/docs) repository.

## Library definition files

The library definition files are plain text files found in the `library/`
subfolder of the official-images repository.

### File names

The name of a definition file will determine the name of the image(s) it
creates. For example, the `library/ubuntu` file will create images in the
`<namespace>/ubuntu` repository. If multiple instructions are present in
a single file, all images are expected to be created under a different tag.

### Instruction format

```
<docker-tag>: <git-url>@<git-commit-id>
2.2.0: git://github.com/dotcloud/docker-redis@a4bf8923ee4ec566d3ddc212

<docker-tag>: <git-url>@<git-tag>
2.4.0: git://github.com/dotcloud/docker-redis@2.4.0

<docker-tag>: <git-url>@<git-tag-or-commit-id> <dockerfile-dir>
2.5.1: git://github.com/dotcloud/docker-redis@2.5.1 tools/dockerfiles/2.5.1
```

Stackbrew will fetch data from the provided git repository from the
provided reference. Generated image will be tagged as `<docker-tag>`.
If a git tag is removed and added to another commit, **you should not
expect the image to be rebuilt.** Create a new tag and submit a pull
request instead.

Optionally, if `<dockerfile-dir>` is present, Stackbrew will look for the
`Dockerfile` inside the specified subdirectory instead of at the root
(and `<dockerfile-dir>` will be used as the "context" for the build).

### Creating a new repository

* Create a new file in the library folder. Its name will be the name of your repository.
* Add your tag definitions using the provided syntax (see above).
* Add the following line to the top of the file:
`# maintainer: Your Name <you@email.com> (@github.name)`
* Create a pull request from your git repository to this one. Please be sure to add details as to what your repository does.

### New tag in existing repository that you're the maintainer of

* Add your tag definition using the instruction format documented above.
* Create a pull request from your git repository to this one. Please be sure to add details about what's new, if possible.
* In the pull request, mention the repository's maintainers using the `@` symbol (found in the relevant MAINTAINERS file).

### Change to an existing tag

* Propose a pull request to the origin repository. Don't hesitate to @-mention one of the repository maintainers (found in the relevant MAINTAINERS file).

## Bashbrew

Bashbrew is a set of bash scripts for cloning, building, tagging, and pushing
the Docker official images. See [`README.md` in the `bashbrew/`
subfolder](bashbrew/README.md) for more information.
