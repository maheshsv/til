# Lean Docker Image with Multi-stage Build

Docker supports multi-stage build since version 17.05. Official documentation can be found [here](https://docs.docker.com/engine/userguide/eng-image/multistage-build/).

There is a good [post](https://lekum.org/post/multistage-dockerfile/) about how it works in terms of building python images.

Unfortunately the image there only contains a `pycryto` package. And then I go ahead and created a simple flask app and put it in a lean docker images, built with multi-stage build. You can find the example in my [github](https://github.com/guihaojin/docker-multi-stage-build-flask).

Google also provided [distroless](https://github.com/GoogleCloudPlatform/distroless), which are lean base images for different languages. The reason I didn't use it is that the python image doesn't include `/bin/bash` and some other commands. But for applications in `Go`, it might be a good idea.
