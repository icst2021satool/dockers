FROM openjdk:8

RUN echo 'alias la="ls -lha"' >> ~/.bashrc

RUN apt-get update && \
	apt-get install -y python3-numpy && \
	apt-get install -y maven && \
	apt-get install -y build-essential && \
	apt-get install -y libxml2-utils && \
	apt-get install -y wget && \
    curl -L https://cpanmin.us | perl - App::cpanminus

WORKDIR /PPgSI

# Install defects4j
RUN git clone https://github.com/rjust/defects4j.git
WORKDIR /PPgSI/defects4j
RUN cpanm --installdeps . && \
	./init.sh
ENV PATH="${PATH}:/PPgSI/defects4j/framework/bin"

WORKDIR /PPgSI

# Clone subsumption experiment repository
RUN apt install vim -y
RUN git clone https://github.com/icst2021satool/subsumption-experiment.git

# Enable script to run
WORKDIR /PPgSI/subsumption-experiment/scripts

RUN chmod +x *.sh

# Checkout Defects4J versions
RUN ./checkoutbatch.sh

# Expand coverage data generate by Jaguar
RUN ./expandbatch.sh
