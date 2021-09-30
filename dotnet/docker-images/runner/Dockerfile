FROM ubuntu:20.04

# argument required by tzdata installation from software-properties-common
ARG DEBIAN_FRONTEND=noninteractive
ARG DOTNET_VERSION
ARG IS_CI

RUN set -x; \
	apt update; \
	apt install -y git \
		curl \
		wget; \
	# Install latest .NET Core SDK
	wget https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb; \
	dpkg -i packages-microsoft-prod.deb; \
	apt-get update; \
	apt-get install -y apt-transport-https; \
	apt-get update; \
	apt-get install -y dotnet-sdk-${DOTNET_VERSION}; \
	# install PowerShell
	apt update; \
	apt install -y powershell; \
	if [ "${IS_CI}" = "true" ]; then \
	else \
		# install/update 7z
		apt install p7zip-full p7zip-rar; \
		# install GitHub CLI for GitHub release
		GH_CLI_VERSION=`curl  "https://api.github.com/repos/cli/cli/releases/latest" | grep '"tag_name"' | sed -E 's/.*"([^"]+)".*/\1/' | cut -c2-`; \
		wget https://github.com/cli/cli/releases/download/v${GH_CLI_VERSION}/gh_${GH_CLI_VERSION}_linux_amd64.tar.gz; \
		tar xvf gh_${GH_CLI_VERSION}_linux_amd64.tar.gz; \
		cp gh_${GH_CLI_VERSION}_linux_amd64/bin/gh /usr/local/bin/; \
		rm -rf gh_${GH_CLI_VERSION}_linux_amd64 gh_${GH_CLI_VERSION}_linux_amd64.tar.gz; \
	fi; \
	# add dev non-root user
	useradd --shell /bin/bash --create-home runner;

USER runner
	
# Built with ❤ by [Pipeline Foundation](https://pipeline.foundation)
