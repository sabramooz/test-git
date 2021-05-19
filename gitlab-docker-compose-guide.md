## Minimum system requirement
- 2 core CPU
- 4 GB RAM


sudo yum install -y yum-utils

sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo

sudo yum install docker-ce docker-ce-cli containerd.io

sudo systemctl start docker

sudo docker run hello-world

export GITLAB_HOME=/srv/gitlab

sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

docker-compose --version

vim docker-compose.yml

### Create a docker-compose.yml

web:
  image: 'gitlab/gitlab-ce:latest'
  restart: always
  hostname: 'gitlab.yourdomain.com'
  environment:
    GITLAB_OMNIBUS_CONFIG: |
      external_url 'https://gitlab.yourdomain.com'
  ports:
    - '80:80'
    - '443:443'
    - '22:23'
  volumes:
    - '/srv/gitlab/config:/etc/gitlab'
    - '/srv/gitlab/logs:/var/log/gitlab'
    - '/srv/gitlab/data:/var/opt/gitlab'
    
docker-compose up -d

wait 10 minutes

use ip in a browser to set up your Gitlab


Troubleshouting

docker exec -it gitlab vim /etc/gitlab/gitlab.rb

docker exec -it gitlab update-permissions

docker exec -it root_web_1 vim /etc/gitlab/gitlab.rb

monitoring['grafana']['enable'] = false

docker restart gitlab
