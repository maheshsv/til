# Lean Docker Image with Multi-stage Build

Docker supports multi-stage build since version 17.05. You can check the [documentations](https://docs.docker.com/engine/userguide/eng-image/multistage-build/).

There is a good [post](https://lekum.org/post/multistage-dockerfile/) about how it works when building python images.

Unfortunately the image there only contains a `pycryto` package. And then I go ahead and created a simple flask app and put it in a lean docker images. You can find the example in my [github](https://github.com/guihaojin/docker-multi-stage-build-flask).

Google also provided [distroless](https://github.com/GoogleCloudPlatform/distroless), which are lean base images for different languages.
