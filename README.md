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

It is highly recommended that you browse some of the existing `library/` file contents (and history to get a feel for how they change over time) before creating a new one to become familiar with the prevailing conventions and further help streamline the review process (so that we can focus on content instead of esoteric formatting or tag usage/naming).

### Filenames

The filename of a definition file will determine the name of the image repository it creates on the Docker Hub. For example, the `library/ubuntu` file will create tags in the `ubuntu` repository.

### Instruction format

	<docker-tag>: <git-url>@<git-commit-id>
	
	4.1.1: git://github.com/docker-library/wordpress@bbef6075afa043cbfe791b8de185105065c02c01
	4.1: git://github.com/docker-library/wordpress@bbef6075afa043cbfe791b8de185105065c02c01
	4: git://github.com/docker-library/wordpress@bbef6075afa043cbfe791b8de185105065c02c01
	latest: git://github.com/docker-library/wordpress@bbef6075afa043cbfe791b8de185105065c02c01
	
	
	<docker-tag>: <git-url>@<git-commit-id> <dockerfile-dir>
	
	2.6.17: git://github.com/docker-library/redis@062335e0a8d20cab2041f25dfff2fbaf58544471 2.6
	2.6: git://github.com/docker-library/redis@062335e0a8d20cab2041f25dfff2fbaf58544471 2.6
	
	2.8.19: git://github.com/docker-library/redis@062335e0a8d20cab2041f25dfff2fbaf58544471 2.8
	2.8: git://github.com/docker-library/redis@062335e0a8d20cab2041f25dfff2fbaf58544471 2.8
	2: git://github.com/docker-library/redis@062335e0a8d20cab2041f25dfff2fbaf58544471 2.8
	latest: git://github.com/docker-library/redis@062335e0a8d20cab2041f25dfff2fbaf58544471 2.8
	
	experimental: git://github.com/tianon/dockerfiles@90d86ad63c4a06b7d04d14ad830381b876183b3c debian/experimental

Bashbrew will fetch code out of the Git repository at the commit specified here. The generated image will be tagged as `<manifest-filename>:<docker-tag>`.

Using Git tags instead of explicit Git commit references is supported, but heavily discouraged. For example, if a Git tag is changed on the referenced repository to point to another commit, **the image will not be rebuilt**. Instead, either create a new tag (or reference an exact commit) and submit a pull request.

Optionally, if `<dockerfile-dir>` is present, Bashbrew will look for the `Dockerfile` inside the specified subdirectory instead of at the root (and `<dockerfile-dir>` will be used as the ["context" for the build](https://docs.docker.com/reference/builder/)).

### Creating a new repository

-	Create a new file in the `library/` folder. Its name will be the name of your repository on the Hub.
-	Add your tag definitions using the appropriate syntax (see above).
-	Add a line similar to the following to the top of the file:

		# maintainer: Your Name <your@email.com> (@github.name)

-	Create a pull request adding the file from your forked repository to this one. Please be sure to add details as to what your repository does.

### Adding a new tag in an existing repository (that you're the maintainer of)

-	Add your tag definition using the instruction format documented above.
-	Create a pull request from your Git repository to this one. Please be sure to add details about what's new, if possible.
-	In the pull request comments, feel free to prod the repository's maintainers (found in the relevant `MAINTAINERS` file) using GitHub's @-mentions.

### Change to a tag in an existing repository (that you're the maintainer of)

-	Update the relevant tag definition using the instruction format documented above.
-	Create a pull request from your Git repository to this one. Please be sure to add details about what's changed, if possible.
-	In the pull request comments, feel free to prod the repository's maintainers (found in the relevant `MAINTAINERS` file) using GitHub's @-mentions.

## Bashbrew

Bashbrew is a set of bash scripts for cloning, building, tagging, and pushing
the Docker official images. See [`README.md` in the `bashbrew/`
subfolder](bashbrew/README.md) for more information.
