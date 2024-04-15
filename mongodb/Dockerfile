# Start with a Wolfi base image
FROM ghcr.io/chainguard-images/static:latest as builder

# Install Melange
RUN apk add melange

# Set up the working directory
WORKDIR /build


# Clone the MongoDB repository
RUN git clone --depth 1 --branch v7.3 https://github.com/mongodb/mongo.git

# Change to the MongoDB source directory
WORKDIR /build/mongo

# Use Melange to install dependencies
# Note: Adjust the following command based on the actual dependencies of MongoDB
# This is a placeholder for demonstration purposes
RUN melange install 

# Compile MongoDB from source
# The actual commands depend on MongoDB's build system (e.g., SCons)
RUN <your-build-command>



# Start with a clean Wolfi image for the final build
FROM ghcr.io/chainguard-images/static:latest

# Copy the compiled MongoDB binaries from the builder image
COPY --from=builder /build/mongo/<path-to-compiled-binaries> /usr/local/bin/

# Set up environment variables, ports, and default command
ENV PATH=/usr/local/bin:$PATH
EXPOSE 27017

CMD ["mongod"]

