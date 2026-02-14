#!/bin/bash

# Update system
dnf update -y

# Install Java (Jenkins requirement)
dnf install -y java-17-amazon-corretto

# Add Jenkins repo
wget -O /etc/yum.repos.d/jenkins.repo \
  https://pkg.jenkins.io/redhat-stable/jenkins.repo

rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key

# Install Jenkins
dnf install -y jenkins

# Start and enable Jenkins
systemctl enable jenkins
systemctl start jenkins

# Open port 8080 (if firewalld is running)
systemctl start firewalld
firewall-cmd --permanent --add-port=8080/tcp
firewall-cmd --reload
