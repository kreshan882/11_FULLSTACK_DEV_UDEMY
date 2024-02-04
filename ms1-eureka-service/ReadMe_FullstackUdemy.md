## 1) Eureka service MS
 - runn first
 
 
 
## 2) Resturent Listing MS
  - mapstruct: DTO to Entity converter (Using Lambda expression)
  - min 8/29
  
## 4) food catalog
	- done
	
## 5) order servic mongo Db
	11-19/28 min
	Mongo Db compass --> create new Db working
	
## 6) anguler app
		20) 0/9 min
		
#5 Docker
 - create docker image and push to Docker hub
 
 1) start docker desktop
 2) docker hub name:kreshan88 (https://hub.docker.com/) gmail+ pw#1 
 
 3) -------> image create localy
    cd D:\11_FULLSTACK_DEV_UDEMY\ms1-eureka-service/
    mvn clean install   (create jar file)
 	docker build -t kreshan88/udemy-ms1-eureka-service:0.0.1 .
 	docker images   
 	
 	-----> push to docker Hub
 	docker login 
 	docker push kreshan88/udemy-ms1-eureka-service:0.0.1
 	
 4) for all outher service
    docker build -t kreshan88/udemy-ms2-restaurant-listing:0.0.1 .
    docker build -t kreshan88/udemy-ms3-user-service:0.0.1 .
    docker build -t kreshan88/udemy-ms4-food-catalogue:0.0.1 .
    docker build -t kreshan88/udemy-ms5-order-service:0.0.1 .
    
    
    docker push kreshan88/udemy-ms2-restaurant-listing:0.0.1
    docker push kreshan88/udemy-ms3-user-service:0.0.1
    docker push kreshan88/udemy-ms4-food-catalogue:0.0.1
    docker push kreshan88/udemy-ms5-order-service:0.0.1
    docker push kreshan88/udemy-angular-food-delivery-app:0.0.1
    
 5) angular service 
 	cd D:\11_FULLSTACK_DEV_UDEMY\angular-food-delivery-app/
 	ng build    --( create dist/ with 6 files)
 	docker build -t kreshan88/udemy-angular-food-delivery-app:0.0.1 .
 	docker push kreshan88/udemy-angular-food-delivery-app:0.0.1
 	
 	
============================ with AWS Cloude Config=================
    cd D:\11_FULLSTACK_DEV_UDEMY\ms2-restaurant-listing/
    mvn clean install   
	docker build -t kreshan88/udemy-ms1-eureka-service:latest .  
 	docker push kreshan88/udemy-ms1-eureka-service:latest
	
 	docker build -t kreshan88/udemy-ms2-restaurant-listing:latest .  
 	docker push kreshan88/udemy-ms2-restaurant-listing:latest
 	
 	docker build -t kreshan88/udemy-ms3-user-service:latest .  
 	docker push kreshan88/udemy-ms3-user-service:latest
 	
 	docker build -t kreshan88/udemy-ms4-food-catalogue:latest .  
 	docker push kreshan88/udemy-ms4-food-catalogue:latest
 	
 	docker build -t kreshan88/udemy-ms5-order-service:latest .  
 	docker push kreshan88/udemy-ms5-order-service:latest
 	
 	
# 7) AWS
					
 7.1) INSTALL CHOCOLATEY ==> software install--> ( https://chocolatey.org/install )
	Power Shell+ run As admin-> SCRIPT_FOR_INSTALL [copy from above) ---> installes suess 
	SCRIPT_FOR_INSTALL : >> Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
	>> choco  ---> Chocolatey v2.2.2
	
					
 7.2) INSTALL KUBECTL ( power Shell -> run As Admin)
		>> choco install kubernetes-cli  (for cubectl)					
	    >> choco install awscli          (for aws)
 	    >> choco install eksctl          (for eksctl)

 	   
 7.3) connect IAM user using CMD
 		>> aws configure  ====> access key| security kry| region
 		>> aws sts get-caller-identity  (verifi user login)
 		
 7.4) CREATE cluster types
 		1) eksctl create cluster (create cluster with default parameter)
 		2) eksctl create cluster -f cluster.yml (using yml file
 		
 		3) eksctl create cluster --name aws-eks-cluster-k --region ap-southeast-1 --nodegroup-name eks-cluster-node --node-type t3.medium --nodes 1
 				====>> created success [AWS -> EKS ->  can see the [aws-eks-cluster-k] name in GUI ]
 				====> take 20 min to complete
 		
#8) Cloude database
	===> RDS-Mysql
		create+ add inbound rule + connrct with workbencg
	
		spring-datasource
    	url: jdbc:mysql://localhost:3306/udemy_fs_restaurantdb
    	url: mysql-db-instance.c508c0mq2kr1.ap-southeast-1.rds.amazonaws.com:3306/udemy_fs_restaurantdb
    	admin| password
	
	===>Mongo DB
		https://www.mongodb.com/cloud/atlas
		URL-ENCODED = Password#1 ==Password%231
		mongodb+srv://admin:<password>@udemy-cluster.v69bwyk.mongodb.net/
		mongodb+srv://admin:Password%231@udemy-cluster.v69bwyk.mongodb.net/
		

#9) Kurbernets		
		
		
		
		tasource:
    url: jdbc:mysql://localhost:3306/udemy_fs_restaurantdb
    url: mysql-db-instance.c508c0mq2kr1.ap-southeast-1.rds.amazonaws.com:3306/udemy_fs_restaurantdb 		
 		
#10) creat Manifest.yml file , and run it in local, connect with AWS
	cd D:\11_FULLSTACK_DEV_UDEMY\deployment-folder-k\aws
	aws configure
	kubectl apply -f .
	kubectl get pods
	kebectl logs (podId)
	
	==> run eureks service same as local [ http://localhost:8761/ ]
		kubectl port-forward service/eureka-service 8761:8761
	
	== test order servise same as local
	kubectl port-forward service/restaurant-service 9091:9091
	kubectl port-forward service/user-service 9093:9093
	kubectl port-forward service/foodcatalogue-service 9092:9092
	kubectl port-forward service/order-service 9094:9094
	POSTMAN ---> send request working good
	
12) Install ALB Controller
	Amason Guid https://docs.aws.amazon.com/eks/latest/userguide/aws-load-balancer-controller.html:
    12.1) Download [cd C:\Users\KRESHAN88\Desktop\UDEMY_AWS]
    	https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.4.7/docs/install/iam_policy.json
    	
    12.2)    	aws iam create-policy --policy-name AWSLoadBalancerControllerIAMPolicy --policy-document file://iam_policy.json --region ap-southeast-1
			
	12.3) eksctl utils associate-iam-oidc-provider --region=ap-southeast-1 --cluster=aws-eks-cluster-k --approve
	
	12.4) Create role [YOUR_AWS_ACCOUNT_ID: iam user account ID arn:aws:iam::730335579537:user/KRESHAN_EKS)
		>> eksctl create iamserviceaccount --cluster=aws-eks-cluster-k --namespace=kube-system --region ap-southeast-1 --name=aws-load-balancer-controller --role-name AmazonEKSLoadBalancerControllerRole --attach-policy-arn=arn:aws:iam::730335579537:policy/AWSLoadBalancerControllerIAMPolicy --approve
		
	12.5) add certificate
		kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v1.5.4/cert-manager.yaml
		
	--12.6) download AWS Load Balancer Controlle[Download the controller specification]
		curl -Lo v2_5_4_full.yaml https://github.com/kubernetes-sigs/aws-load-balancer-controller/releases/download/v2.5.4/v2_5_4_full.yaml
	
	cd D:\11_FULLSTACK_DEV_UDEMY\deployment-folder-k\ingress controller
	12.6.1) remove [ServiceAccount] in (6) filer
		add [your-cluster-name] 
		add region
		add vpc-04877cb38a033e382	
		
	12.6.2) run the file	
	kubectl apply -f v2_5_4_full-modified.yam
	
	12.6.3) verified 
		kubectl get pods -n kube-system ------> fail
		
	--12.7) when faile occered in (12.6)
			cd D:\11_FULLSTACK_DEV_UDEMY\deployment-folder-k\ingress controller
			kubectl apply -f v2_4_7_full_modified.yaml
			kubectl get pods -n kube-system  -------------> running success
	
	12.7) cd D:\11_FULLSTACK_DEV_UDEMY\deployment-folder-k\aws2
		  kubectl apply -f ingress.yml
		  kubectl get ingress	   ---> get domain name
		  
	12.8) REst Service working good\
			http://k8s-default-awsingre-b3376c6fd9-962534291.ap-southeast-1.elb.amazonaws.com/restaurant/fetchById/1	[5min/19]
	
	
	12.9) anguler run\
			cd D:\11_FULLSTACK_DEV_UDEMY\angular-food-delivery-app
			ng build
			ng serve ----> http:localhost:4200 success test
			docker build -t kreshan88/udemy-angular-food-delivery-app:latest .  
 			docker push kreshan88/udemy-angular-food-delivery-app:latest
 			
 			cd D:\11_FULLSTACK_DEV_UDEMY\deployment-folder-k\aws2
 			kubectl apply -f angular-manifest.yml
 			
#14) EC2 installation 
		Create EC2 instance
		Connect EC2 Instance
		run below comment
			sudo yum update
	        sudo yum install -y maven
	        mvn -version	
	        
	        JDK11
	        sudo yum install java-11-amazon-corretto-headless
	        
	        DOCKER
	        sudo yum update -y
        	sudo yum install -y docker
        	sudo service docker start    ---> docker demon start
        	sudo chkconfig docker on		---> start docker auto when system boot	
        	
        	JENKINE
        	sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo  ----> download, and add to yum
        	sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key    ---> download key
        	sudo yum install jenkins -y
        	sudo systemctl enable jenkins   ---> jenkin start auto , when ec2 instance boot
        	sudo systemctl start jenkins    ---> start genkine
        	
        	GIT
        	sudo yum install -y git
        	
        	SONAR
        	>>sudo su
        	# docker run -d -p 9000:9000 --name sonarqube sonarqube  ---> run in docker container
        	# docker logs -f sonarqube     
        	---> http://(ec2_instance_public_ip):9000 ---- http://54.169.220.190:9000 | Un:admin pw:admin-> Password#1 
        	
        	SONAR_TOKEN
        	SonarGui->myAccount->Secure->sonarToken|userToken|noExpire-> Generate
        	squ_b1bb907c46d7767a0498f4468a4d81e752d02d73 
        	
        	SCAN PROJECT ON SONAR
        	cd D:\11_FULLSTACK_DEV_UDEMY\ms2-restaurant-listing/
        	mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent install sonar:sonar -Dsonar.host.url=http://54.169.220.190:9000/ -Dsonar.login=squ_b1bb907c46d7767a0498f4468a4d81e752d02d73
        	====> Sonar Gui can see the report
        		  GUI-> project -> pass
        	
        	
#15) CICD Configuration
		   1) Jenkine configuration
		   		sudo su
		   		systemctl status jenkines
		   		http://54.169.220.190:8080  --> success (need to get password)
		   		cat /var/lib/jenkins/secrets/initialAdminPassword  ---> get password [c3fec8c45be24f3abb154a63c8f7e73a]
		   		
        	3) Install webHook in Jenkine
        			https://github.com/kreshan882/ms2-restaurant-listing.git
        			
        			Add webHook in GitGub
        			Generate SSL key In Jenkin        
        					ssh-keygen -t rsa -b 4096
        					cat ~/.ssh/id_rsa.pub	  ----> Send to github[ kreshan--> settings-> SSH & GPG key
        					                       -> new SSH key[jenkines-publik-ket| authgndication| key] ---> add success 
        					cat ~/.ssh/id_rsa  ----> add private key to jenkine(for git-hub | docker)
        							GITHUB---> id:git-ssh
        							DOCKER --> id:DOCKER_HUB_CREDENTIAL 
        						          
        					
  15.87) Argo CD install [GUID: https://argo-cd.readthedocs.io/en/stable/getting_started/ ]
  		RUN IN LOCAL [C:\Users\KRESHAN88>]
  		1) kubectl create namespace argocd
		2) kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
  		3) kubectl port-forward service/argocd-server -n argocd 8080:80
  		----> can load http://localhost:80 ---> not working
  		
  		==> after install (6)
  		4) argocd admin initial-password -n argocd  ---> un:admin | get password hear
  		        					
        FOR DELETE ARGO CD FULL
        5) kubectl delete -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml					
        
        CRGOCD_Commend LINE
        6) choco install argocd-cli
        
        
#16) delete instance
		1) delete eks cluster (cluster+ auto created EC2)
				eksctl delete cluster --name aws-eks-cluster-k --region ap-southeast-1
				
		2) delete ec2 instance manuwaly (CICD)
		
		3) delete RDS (for mysql)
				manuwal delete
		
		

        					         