FROM openjdk:8

RUN echo 'alias la="ls -lha"' >> ~/.bashrc

RUN apt-get update && \
	apt-get install -y python3-numpy && \
	apt-get install -y maven && \
	apt-get install -y build-essential && \
	apt-get install -y libxml2-utils && \
	apt-get install -y wget && \
    curl -L https://cpanmin.us | perl - App::cpanminus

WORKDIR /stvr

# Install defects4j
RUN git clone https://github.com/rjust/defects4j.git
WORKDIR /stvr/defects4j
RUN cpanm --installdeps . && \
	./init.sh
ENV PATH="${PATH}:/stvr/defects4j/framework/bin"

WORKDIR /stvr

# Clone fault detection ability experiment repository
RUN apt install vim -y
RUN git clone https://github.com/icst2021satool/probabilistic-coupling-experiment.git

# Enable script to run
WORKDIR /stvr/probabilistic-coupling-experiment/datacollection/src

RUN chmod +x *.sh

# Checkout coverage data from public repository
#RUN ./checkoutcoverage.sh

# Expand coverage data generate by Jaguar
#RUN ./expandbatch.sh
