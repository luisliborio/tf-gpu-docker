# base image
FROM tensorflow/tensorflow:2.17.0-gpu

RUN apt-get update && apt-get install -y graphviz

RUN pip install --upgrade pip


# JAVA for pyspark
RUN apt install openjdk-17-jdk -y

# Fix the blinker conflict with mlflow before installing requirements
RUN pip install --ignore-installed blinker
# Install any needed packages specified in requirements.txt
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# # If installing gymnasium[all]
# # RUN apt-get install -y swig

# #######################################################
# opencv dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    cmake \
    pkg-config \
    libjpeg-dev \
    libpng-dev \
    libtiff-dev \
    libavcodec-dev \
    libavformat-dev \
    libswscale-dev \
    libv4l-dev \
    libxvidcore-dev \
    libx264-dev \
    libgtk2.0-dev \
    libgtk-3-dev \
    libatlas-base-dev \
    gfortran \
    && rm -rf /var/lib/apt/lists/*

RUN pip install --no-cache-dir opencv-python-headless
# #######################################################

# Make port 8888 available to the world outside this container
EXPOSE 8888

# Keep the container running
CMD ["tail", "-f", "/dev/null"]
