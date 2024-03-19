## Dockerfile
#### 1. openssh-server
    Allows ssh/sftp/scp service working.
#### 2. useradd
    Create new user. Can replace sftp_user to any of your custom name. (Make sure to replace all of the sftp_user).
#### 3. chpasswd
    Change password for sftp_user. The YOURPASSWORDHERE need to be replaced by any secure password.
#### 4. /var/run/sshd
    RUN mkdir -p /var/run/sshd is a necessary file for sshd.
#### 5. sed on line 13 
    Keeps session alive
#### 6. Line 15 & 16
    Then there is ENV NOTVISIBLE “in users profile” and RUN echo “export VISIBLE=now” >> /etc/profile. These two lines is necessary for sshd to get it working in docker.
#### 7. Line 19
    CMD [“/usr/sbin/sshd”, “-D”] is to run sshd in daemon (background) mode.

#### 8. Setup folders and permissions
    Then it setup for the sftp folders.
    Then it only allow for sftp connection without allowing ssh at the /etc/ssh/sshd_config file. 
    
#### 9. Build docker image
    docker build -t local-sftp-container .

#### 10. Run the container
    docker run -d -p 2036:22 local-sftp-container
    (any free host:sftp port 22)

#### 11. Connect to sftp container
    sftp -oPort=2036 sftp_user@127.0.0.1


