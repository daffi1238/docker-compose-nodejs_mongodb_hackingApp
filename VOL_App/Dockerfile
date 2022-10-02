##Start container:
##

## Delete image
## sudo docker rmi docker_kali_linux

# Kali Linux latest with useful tools by tsumarios
FROM kalilinux/kali-rolling

# Set working directory to /root
WORKDIR /root/app

# Copy the app to the container
COPY package.json ./
COPY server.js .
COPY app ./

# Update
RUN apt -y update && DEBIAN_FRONTEND=noninteractive apt -y dist-upgrade && apt -y autoremove && apt clean

# Install common and useful tools
RUN apt -y install curl wget vim git net-tools whois netcat-traditional pciutils usbutils

# Install useful languages
RUN apt -y install python3-pip golang nodejs npm

# Install Kali Linux "Top 10" metapackage and a few cybersecurity useful tools
#RUN DEBIAN_FRONTEND=noninteractive apt -y install kali-tools-top10 exploitdb man-db dirb nikto wpscan uniscan lsof apktool dex2jar ltrace strace binwalk

# Install Tor and proxychains, then configure proxychains with Tor
#RUN apt -y install tor proxychains
#COPY config/proxychains.conf /etc/proxychains.conf

# Install ZSH shell with custom settings and set it as default shell
#RUN apt -y install zsh
#RUN sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
#COPY config/.zshrc .

## Install de dependencies for the application
RUN npm install

##ENTRYPOINT ["/bin/zsh"]

# Bundle app source
COPY . .
EXPOSE 3000
CMD [ "node", "app.js" ]