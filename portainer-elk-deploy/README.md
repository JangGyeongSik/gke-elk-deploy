# Log Collect System ES Configuration

### VPC, Subnet F/W & Server 구축 
 - VPC
   - vpc-prod-es 
 - Subnet
   - ipCidrRange: 10.x.x.x/25 
 - Proxy-Only Subnet
   - ipCidrRange: 10.x.x.x/26
 - GCE
    #### Portainer Agent Connnection w/GCP
    - docker-manager-01 
    - docker-manager-02
    - docker-manager-03
 	#### ES-MASTER-01, ES-METRICBEAT-01 
 	 - docker-worker-01 ( es-master-01 )  asia-northeast3-a
 	 - docker-worker-01 ( es-metricbeat-01 )
 	#### ES-MASTER-02,03
 	 - docker-worker-02 ( es-master-02 )  asia-northeast3-a
 	 - docker-worker-03 ( es-master-03 )  asia-northeast3-c
 	#### ES-DATA-01, ES-INGEST-01
 	 - docker-worker-04 ( es-data-01, data )  asia-northeast3-a -> Additional Disk 5TiB 
 	 - docker-worker-04 ( es-ingest-01, ingest ) asia-northeast3-a
 	#### ES-DATA-02, ES-COORDINATE-01 
 	 - docker-worker-05 ( es-data-02, data )  asia-northeast3-a -> Additional Disk 5TiB
 	 - docker-worker-05 ( es-coordinate-01, coordinate ) asia-northeast3-a
 	#### ES-DATA-03, ES-COORDINATE-02 
 	 - docker-worker-06 ( es-data-03, data )  asia-northeast3-c  -> Additional Disk 5TiB
 	 - docker-worker-06 ( es-coordiante-02, coordinate )  asia-northeast3-a 
 	#### ES-DATA-04, ES-KIBANA-01
  	 - docker-worker-07 ( es-data-04, data )  asia-northeast3-c  -> Additional Disk 5TiB
 	 - docker-worker-07 ( es-kibana-01, kibana ) asia-northeast3-c  
 	#### ES-DATA-05, 
 	- docker-worker-08 ( es-data-05, data )  asia-northeast3-c  -> Additional Disk 5TiB



### Docker Swarm Mode 구성 진행 
  - Docker Swarm Mode 구성
  	- docker swarm init --advertise-addr MANAGER_NODE_IP ( vm-prod-docker-manager-01 IP )
  - Worker 등록 
  	- docker swarm join --token SWARM_WORKER_TOKEN MANAGER_NODE_IP:2377 ( Worker )
  - Manager 등록
  	- docker swarm join --token SWARM_MANAGER_TOKEN MANAGER_NODE_IP:2377 ( Manager )

3. Portainer 연동
4. ELK Stack Configuration with Docker Compose.. 
5. ES ILB 구성 
   - ES_DOMAIN:9200 ( ES_ILB:9200 )
   - KIBANA_DOMAIN:443 ( KIBANA_ILB:443)