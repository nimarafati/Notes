FROM mambaorg/micromamba:0.15.2

# Select the shell to use.
SHELL ["/bin/bash", "-c"]

# Add metadata to the container using labels.
LABEL description="Spade (Search for Patterned DNA Elements) container" \
      author="Mahesh Binzer-Panchal" \
      version="1.0.0"

# Change user to root to install things (set to micromamba in base image)
USER root

# Update and install software dependencies
# with APT (Advanced Packaging  Tool)
RUN apt-get update && \
    apt-get install -y procps ghostscript git

# Install tools using the mamba package manager
RUN micromamba install -y -n base -c conda-forge -c bioconda\
        python=3.7.10 \
        mafft=7.487 \
        blast=2.12.0 \
        openssl=1.1.1l \
        perl-bioperl=1.7.2 && \
    micromamba clean --all --yes

# Manual installation in another directory
WORKDIR /opt
RUN git clone --depth 1 https://github.com/yachielab/SPADE && \
    cd SPADE && chmod u+x *.py && \
    pip install matplotlib==2.2.3 && \
    pip install seaborn==0.8.1 && \
    pip install weblogo==3.6.0 && \
    pip install biopython

ENV PATH="/opt/SPADE:${PATH}"

CMD [ "SPADE.py" ]
