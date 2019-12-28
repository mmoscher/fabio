# Docker Hub Hooks

To perform an automated multiarch build using Docker-Hub we need to utilize 
[Custom build phase hooks](https://docs.docker.com/docker-hub/builds/advanced/#custom-build-phase-hooks).

We implement the `pre_build` and `post_build` hooks. Each of them is explained in more detail next.

#### pre_build custom hook

#### post_push custom hook


# Idea and Resource
This implementation of multiarch builds using Docker-Hub follows the example [ckulka/docker-multi-arch-example
](https://github.com/ckulka/docker-multi-arch-example) by [@ckulka](https://github.com/ckulka)