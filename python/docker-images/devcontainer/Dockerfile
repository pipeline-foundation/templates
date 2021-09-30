FROM ubuntu:20.04

# argument required by tzdata installation from software-properties-common
ARG DEBIAN_FRONTEND=noninteractive

RUN apt update; \
	apt install -y git \
			wget \
			curl; \
	# clean install Python3.10
	apt install -y build-essential \
		zlib1g-dev \
		libncurses5-dev \
		libgdbm-dev \
		libnss3-dev \
		libssl-dev \
		libreadline-dev \
		libffi-dev \
		libsqlite3-dev \
		libbz2-dev; \
	wget https://www.python.org/ftp/python/3.10.0/Python-3.10.0.tgz; \
	tar -xf Python-3.10.0.tgz; \
	( \
		cd Python-3.10.0 || exit; \
		./configure --enable-optimizations; \
		make -j 12; \
		make altinstall; \
	); \
	rm -rf Python-3.10.0.tgz Python-3.10.0; \
	# install pip for Python3.10
	curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py; \
	python3.10 get-pip.py; \
	rm -rf get-pip.py; \
	# install flake8
	pip install flake8; \
	# add dev non-root user
	useradd --shell /bin/bash --create-home devcontainer;

USER devcontainer

CMD ["bash"]

# Built with ❤ by [Pipeline Foundation](https://pipeline.foundation)
