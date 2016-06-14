FROM lamuguo/jsonnet:latest

WORKDIR /opt

RUN apt-get install -y wget automake python openjdk-8-jdk

# Setup JDK
RUN ln -s /usr/lib/jvm/java-8-openjdk-amd64 /usr/lib/jvm/default-java

# install protoc
RUN git clone https://github.com/google/protobuf
RUN git clone https://github.com/grpc/grpc-java

# install googletest tags/release-1.7.0
RUN git clone https://github.com/google/googletest && \
    cd googletest && git checkout tags/release-1.7.0 && cd ..

# install protoc
RUN cd protobuf && \
    git checkout tags/v3.0.0-beta-3 && \
    ln -s ../googletest gmock && \
    ./autogen.sh && \
    ./configure && \
    make && \
    make install && \
    export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH && \
    export PATH=/usr/local/bin:$PATH && \
    cd ..

# install grpc-java plugin
RUN cd grpc-java && git checkout tags/v0.14.0
RUN ln -s /usr/lib/jvm/java-8-openjdk-amd64 /usr/lib/jvm/default-java
RUN ./gradlew build && ./gradlew install
RUN cd ..
