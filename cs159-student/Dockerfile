# Use an official Python runtime as a parent image
FROM gradescope/auto-builds:ubuntu-18.04 

RUN apt update && \
  apt install -y --no-install-recommends \
  apt-utils vim man less apt-utils git sudo nano emacs \
  python3 build-essential \
  supervisor nginx \
  wget curl locales python3-pip \
  python3-setuptools python3-lxml \
  pandoc

RUN export TZ="/usr/share/zoneinfo/America/Los_Angeles"
RUN ln -fs /usr/share/zoneinfo/Europe/Dublin /etc/localtime

RUN locale-gen en_US.UTF-8

COPY data /cs/cs159/data


#ENV LD_LIBRARY_PATH=/usr/local/lib
#ENV PKG_CONFIG_PATH=/usr/local/lib/pkgconfig

# Install any needed packages specified in requirements.txt
#ENV PYTHONUSERBASE /mnt/vendor
COPY requirements.txt /tmp/requirements.txt
# RUN pip3 install numpy==1.19.4 cython==0.29.21
RUN pip3 install --trusted-host pypi.python.org -r /tmp/requirements.txt
RUN pip3 install -U spacy==2.2.3

# Add spacy en small language model
RUN python3 -m spacy download en


#######################################
# Set Up Student Environment
#######################################

RUN useradd -ms /bin/bash student
RUN echo "student:student" | chpasswd && adduser student sudo

RUN mkdir -p /home/student/nlp
USER student 
WORKDIR /home/student/nlp

