FROM adaickalavan/gocv-debian

#Author label
LABEL Author Adaickalavan Meiyappan



#Install the GoCV package
RUN go get -u -d gocv.io/x/gocv


#Set environment variable for librdkafka
ENV LIBRDKAFKA_VERSION 1.0.0

#Install dev tools
RUN apt-get -y update \
        && apt-get install -y --no-install-recommends upx-ucl zip \
        && apt-get clean \
        && rm -rf /var/lib/apt/lists/*

# Build librdkafka
RUN curl -Lk -o /root/librdkafka-${LIBRDKAFKA_VERSION}.tar.gz https://github.com/edenhill/librdkafka/archive/v${LIBRDKAFKA_VERSION}.tar.gz && \
      tar -xzf /root/librdkafka-${LIBRDKAFKA_VERSION}.tar.gz -C /root && \
      cd /root/librdkafka-${LIBRDKAFKA_VERSION} && \
      ./configure --prefix /usr && make && make install && make clean && ./configure --clean

# Get confluent-kafka-go/kafka library
RUN go get -u github.com/confluentinc/confluent-kafka-go/kafka



# To verify that the Docker image has been built correctly, do the following.
# By enabling the ENTRYPOINT command below, running 
# ```
# docker run <image_name>
# ```
#
# should print the following message:
#
# ```
#gocv version: 0.18.0
#opencv lib version 4.0.0
# ```

# Run the app command by default when the container starts
# ENTRYPOINT ["go", "run", "$GOPATH/src/gocv.io/x/gocv/cmd/version/main.go"]
