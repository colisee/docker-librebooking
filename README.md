This project implements the [librebooking](https://github.com/effgarces/BookedScheduler) web application as a container.

# How to build the image
## Builder: on your local host, Image: on your local host, Platform: single
Run the following commands:
   ```
   LB_RELEASE=2.8.5 # or any other librebooking release
   docker buildx build \
     --tag librebooking:${LB_RELEASE} \
     --build-arg LB_RELEASE=${LB_RELEASE} \
     --output type=docker \
     .
   ```

## Builder: on your local host, Image: on your default registry, Platform: multiple
Run the following commands:
   ```
   LB_RELEASE=2.8.5 # or any other librebooking release
   REGISTRY_USER=your_registry_user
   docker login --username ${REGISTRY_USER}
   docker run --privileged tonistiigi/binfmt -install all
   docker buildx build \
     --tag ${REGISTRY_USER}/librebooking:${LB_RELEASE} \
     --build-arg LB_RELEASE=${LB_RELEASE} \
     --output type=registry \
     --platform=linux/amd64,linux/arm64,linux/arm/v7  \
     .
   ```

## Builder: on github, Image: on docker hub, Platform: multiple
1. Create a github secret, called `REGISTRY_TOKEN`, to store your docker hub token
1. Run the github action `Docker`
1. Specify the librebooking release
1. Seat back and relax

# How to run the image
Refer to file [USAGE.md](USAGE.md)
