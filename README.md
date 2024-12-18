[![GitHub Release](https://img.shields.io/github/v/release/linuxserver/docker-transmission.svg?color=f64747&labelColor=9f9f9f&logoColor=ffffff&style=for-the-badge&logo=transmission)](https://github.com/linuxserver/docker-transmission/releases)

<p align="center">
  <img src="" width="300" title="logo_jf">
</p>

### Requeriments
- Service docker running
  
| Architecture | Available |
| :----: | :----: |
| amd64 | ✅ |
| arm64 | ✅ |
| armhf | ❌ | |
| armv7 | ❌ | |

### Compatible with NAS that have the ability to run docker containers 
| Hardware | Available |
| :----: | :----: |
| Synology | ✅ |
| QNAP | ✅ |
| Asustor | ✅ |


### Install Docker (Ubuntu, Debian, Armbian, DietPi...)
    sudo apt update && sudo apt install git vim wget curl net-tools ca-certificates gnupg -y
    sudo install -m 0755 -d /etc/apt/keyrings
    sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
    sudo chmod a+r /etc/apt/keyrings/docker.asc
    
    echo \
      "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
      $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
      sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    
    sudo apt update && sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
    sudo usermod -aG docker $USER
    sudo reboot

### Clone repo
    git clone https://github.com/azagramac/transmission-docker.git
    cd transmission-docker

### Running
    docker compose up -d

### Output
    $ docker compose up -d
    [+] Running 9/9
     ✔ transmission Pulled                                                                                                                                                                                                                             23.2s 
       ✔ 6d29a096dd42 Pull complete                                                                                                                                                                                                                  4.5s 
       ✔ ac69bd919a82 Pull complete                                                                                                                                                                                                                  5.2s 
       ✔ 2a534069771d Pull complete                                                                                                                                                                                                                  5.7s 
       ✔ 4f4fb700ef54 Pull complete                                                                                                                                                                                                                  5.9s 
       ✔ df1c06f9ce74 Pull complete                                                                                                                                                                                                                 10.6s 
       ✔ f9ec95325cc7 Pull complete                                                                                                                                                                                                                 10.9s 
       ✔ f71b44280505 Pull complete                                                                                                                                                                                                                 21.8s 
       ✔ 8ce81773582a Pull complete                                                                                                                                                                                                                 44.0s 
    [+] Running 2/2
     ✔ Network transmission_default  Created                                                                                                                                                                                                            0.4s 
     ✔ Container transmission        Started

### Check
    docker ps -a

### Logs
    docker logs -f transmission

### Output
    $ docker ps -a
    CONTAINER ID   IMAGE                         COMMAND                CREATED       STATUS                    PORTS                  NAMES
    1ab5d0ec0b2c   linuxserver/transmission:latest     "/transmission/tran…"    34 days ago    Up 2 hours (healthy)                              transmission

### Update image docker
    docker-compose pull transmission

## Add blacklist urls
Edit file settings.json 

    "blocklist-enabled": true,
    "blocklist-url": "http://www.example.com/blocklist",

Restart image docker
    docker restart transmission

### URLs blacklist
    https://github.com/Naunter/BT_BlockLists/raw/refs/heads/master/bt_blocklists.gz
    http://list.iblocklist.com/?list=bt_level1&fileformat=p2p&archiveformat=gz
    http://list.iblocklist.com/?list=bt_level2&fileformat=p2p&archiveformat=gz
    http://list.iblocklist.com/?list=bt_level3&fileformat=p2p&archiveformat=gz

### Dashboard
Open browser
    http://IP_HOST:9091/transmission/web/