/etc/ansible/roles/filebeat-playbook.yml


---
- name: installing and launching filebeat
  hosts: webservers
  become: yes
  tasks:

  - name: download filebeat deb
    command: curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.4.0-amd64.deb

  - name: install filebeat deb
    command: dpkg -i filebeat-7.4.0-amd64.deb

  - name: drop in filebeat.yml
    copy:
      src: /etc/ansible/files/filebeat-config.yml
      dest: /etc/filebeat/filebeat.yml

  - name: enable and configure system module
    command: filebeat modules enable system

  - name: setup filebeat
    command: filebeat setup

  - name: start filebeat service
    command: service filebeat start













/etc/ansible/install-elk.yml


---
- name: Configure Elk VM with Docker
  hosts: elkservers
  remote_user: azadmin
  become: true
  tasks:
   - name: Install docker.io
     apt:
      update_cache: yes
      force_apt_get: yes
      name: docker.io
      state: present
   - name: Install python3-pip3
     apt:
      force_apt_get: yes
      name: python3-pip
      state: present
   - name: Install Docker Module
     pip:
      name: docker
      state: present
   - name: Use more memory
     sysctl:
       name: vm.max_map_count
       value: '262144'
       state: present
       reload: yes
   - name: download and launch a docker web container
     docker_container:
      name: elk
      image: sebp/elk:761
      state: started
      restart_policy: always
      published_ports:
        - 5601:5601
        - 9200:9200
        - 5044:5044


/etc/ansible/files/filebeat-config.yml


#-------------------------- Elasticsearch output -------------------------------
output.elasticsearch:
  # Boolean flag to enable or disable the output module.
  #enabled: true

  # Array of hosts to connect to.
  # Scheme and port can be left out and will be set to the default (http and 9200)
  # In case you specify and additional path, the scheme is required: http://localhost:9200/path
  # IPv6 addresses should always be defined as: https://[2001:db8::1]:9200
  hosts: ["10.1.0.5:9200"]
  username: "elastic"
  password: "changeme"

#============================== Kibana =====================================

# Starting with Beats version 6.0.0, the dashboards are loaded via the Kibana API.
# This requires a Kibana endpoint configuration.
setup.kibana:
  host: "10.1.0.5:5601"
  # Kibana Host
  # Scheme and port can be left out and will be set to the default (http and 5601)
  # In case you specify and additional path, the scheme is required: http://localhost:5601/path
  # IPv6 addresses should always be defined as: https://[2001:db8::1]:5601
  #host: "localhost:5601"







/etc/ansible/my-playbook.yml


--
- name: Config Web VM with Docker
  hosts: webservers
  become: true
  tasks:
  - name: docker.io
    apt:
      update_cache: yes
      name: docker.io
      state: present
  - name: Install pip3
    apt:
      name: python3-pip
      state: present
  - name: Install Docker python module
    pip:
      name: docker
      state: present
  - name: download and launch a docker web container
    docker_container:
      name: dvwa
      image: cyberxsecurity/dvwa
      state: started
      restart_policy: always
      published_ports: 80:80



roulette_dealer_finder_by_time.sh



#!/bin/bash
# This should allow you to search the date and time, and give you the corresponding Roulette dealer.

echo "Enter the date in MMDD format, followed by [enter]:"

read date

grep $date ~/Lucky_Duck_Investigation/Roulette_Loss_Investigation/Dealer_Analysis/RTN | awk -F'["\t" ]' '{print $2, $4, $5, $6, $7}' > ~/Lucky_Duck_Investigation/Roulette_Loss_Investigation/Dealer_Analysis/MACRO |

echo "Enter the time (01-12), followed by [enter]:"

read hour

grep $hour ~/Lucky_Duck_Investigation/Roulette_Loss_Investigation/Dealer_Analysis/MACRO | awk -F'["\t" ]' '{print $2, $3, $4, $5}' > ~/Lucky_Duck_Investigation/Roulette_Loss_Investigation/Dealer_Analysis/MICRO |

echo "Enter AM or PM, followed by [enter]:"

read xm

grep -i $xm ~/Lucky_Duck_Investigation/Roulette_Loss_Investigation/Dealer_Analysis/MICRO | awk -F'["\t" ]' '{print $2, $3, $4}' 

echo "...was the Roulette dealer on" $date "at" $hour $xm






roulette_dealer_finder_by_time_and_game.sh


#!/bin/bash
# This should allow you to search the game, date, time, and give you the corresponding table dealer.

echo "Enter 1 for Black Jack, 2 for Roulette, 3 for Texas Hold'Em, followed by [enter]:"

read game

grep 0 ~/Lucky_Duck_Investigation/Roulette_Loss_Investigation/Dealer_Analysis/DS$game > ~/Lucky_Duck_Investigation/Roulette_Loss_Investigation/Dealer_Analysis/AB |

echo "Enter the date in MMDD format, followed by [enter]:"

read date

grep $date ~/Lucky_Duck_Investigation/Roulette_Loss_Investigation/Dealer_Analysis/AB | awk -F'["\t" ]' '{print $2, $3, $4, $5, $6, $7, $8}' > ~/Lucky_Duck_Investigation/Roulette_Loss_Investigation/Dealer_Analysis/CD |

echo "Enter the time (01-12), followed by [enter]:"

read hour

grep $hour ~/Lucky_Duck_Investigation/Roulette_Loss_Investigation/Dealer_Analysis/CD | awk -F'["\t" ]' '{print $3, $4, $5, $6}' > ~/Lucky_Duck_Investigation/Roulette_Loss_Investigation/Dealer_Analysis/EF |

echo "Enter AM or PM, followed by [enter]:"

read xm

grep -i $xm ~/Lucky_Duck_Investigation/Roulette_Loss_Investigation/Dealer_Analysis/EF | awk -F'["\t" ]' '{print $2, $3, $4}'

echo "...is the table dealer you're looking for on" $date "at" $hour $xm 







system.sh



#!/bin/bash
free -h > ~/backups/freemem/free_mem.txt &&
du -h > ~/backups/diskuse/disk_usage.txt &&
lsof > ~/backups/openlist/open_list.txt &&
df -h > ~/backups/freedisk/free_disk.txt





