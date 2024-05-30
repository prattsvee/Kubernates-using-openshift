# Kubernates-using-openshift



Step 1: Log in to the Developer Sandbox
- Set User Credentials:

  kubectl config set-credentials {username}/{cluster_name} --token={token}
 
- Set Cluster Information:
  
  kubectl config set-cluster {cluster_name} --server={api_server_url}
  
- Set Context:
  
  kubectl config set-context {context} --user={username}/{cluster_name} --namespace={username}-dev --cluster={cluster_name}
  
- Use Context:
  
  kubectl config use-context {context}
  

Step 3: Clone the source code repositories
- Clone quotesweb Repository:
 
  git clone https://github.com/redhat-developer-demos/quotesweb.git
  
- Clone quotemysql Repository:
  bash
  git clone https://github.com/redhat-developer-demos/quotemysql.git
 
- Clone qotd-python Repository:
  bash
  git clone https://github.com/redhat-developer-demos/qotd-python.git
  

Step 4: Create a back-end program called quotes
- Create Quotes Deployment:
  kubectl create -f quotes-deployment.yaml
  
- Create Quotes Service:
  kubectl create -f service.yaml
  
- Create Quotes Route:
  kubectl create -f route.yaml

Step 5: Create a React front-end program called quotesweb
-Create Quotesweb Deployment:
  kubectl create -f quotesweb-deployment.yaml

- Create Quotesweb Service:
  kubectl create -f quotesweb-service.yaml
 
- Create Quotesweb Route:
  kubectl create -f quotesweb-route.yaml


 

Step 6: Scale the back-end app to two pods
- Scale Quotes Deployment:

  kubectl scale deployments/quotes --replicas=3
  

Step 7: Create a Persistent Volume Claim (PVC) for MariaDB
- Create MariaDB PVC:
  kubectl create -f mysqlvolume.yaml
  

Step 8: Create a Secret for the database
- Create MariaDB Secret:
  kubectl create -f mysql-secret.yaml

Step 9: Create a MariaDB database
Create MariaDB Deployment:
  kubectl create -f mysql-deployment.yaml
  

 Step 10: Create and populate the table "quotes" in the "quotesdb" database
- Copy Files and Execute SQL Commands in MariaDB Pod:
  (Multiple `kubectl cp` and `kubectl exec` commands)

Step 11: Update the back-end program to version 2
- Set Environment Variable:
  kubectl set env deployment/quotes DB_SERVICE_NAME=mysql
 
- Update Image of Quotes Deployment:
  kubectl set image deploy quotes quotes=quay.io/donschenck/quotes:v2
  

 Step 12: Destroy the MariaDB pod
-Delete Running MariaDB Pod:
  kubectl delete pod ${podname}


