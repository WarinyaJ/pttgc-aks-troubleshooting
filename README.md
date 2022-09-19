# pttgc-aks-troubleshooting
1. Go to [Azure_Portal](https://azure.microsoft.com/en-us/get-started/azure-portal/) then search kubernetes and select Kubernetes services

<img width="1158" alt="Screen Shot 2565-08-24 at 13 42 46" src="https://user-images.githubusercontent.com/46469458/186349099-679fc9f0-0c51-41f7-baf9-39454eeda184.png">

2. At Kubernetes serices page click on your kubernetes cluster name

<img width="1127" alt="image" src="https://user-images.githubusercontent.com/46469458/190913045-ab84d105-bda1-431a-808b-f8773d0e195a.png">

3. Scroll down to Monitoring session and select Insights

<img width="1435" alt="image" src="https://user-images.githubusercontent.com/46469458/190913204-714dc445-2325-4329-b7f3-ec4ce7374c78.png">

4. At Insights page go to Containers tab then click add filters

<img width="969" alt="image" src="https://user-images.githubusercontent.com/46469458/190913646-c9a0a984-83a8-4e24-8459-f516390fb94f.png">

5. Select data

  Select Property = Namespace
  
  <img width="223" alt="image" src="https://user-images.githubusercontent.com/46469458/190913844-323ab5cd-700f-4220-85a1-fb636141953e.png">

  Select value(s) = default
  
  <img width="186" alt="image" src="https://user-images.githubusercontent.com/46469458/190913919-818ca26c-a2b8-48b0-b09e-9116e53cbc2d.png">

6. You will see container status warning, select warning container

<img width="1197" alt="image" src="https://user-images.githubusercontent.com/46469458/190914094-55f28317-0344-474e-ab21-6828d1237a47.png">

7. At right side you will information about your container

![image](https://user-images.githubusercontent.com/46469458/190914387-a5ba3c11-27ba-4777-8960-d7c072db765b.png)

8. In the container information you will see 
  
  Container Status = waiting
  
  Container Status Reason = ImagePullBackOff (or another error code)

![image](https://user-images.githubusercontent.com/46469458/190914660-8d408581-0434-4900-8794-712fdd3aafad.png)

9. Close container information and select Logs then close Queries popup

<img width="710" alt="image" src="https://user-images.githubusercontent.com/46469458/190914871-23313871-92bc-4f6e-a38e-38c2f1cde6ca.png">

10. At query tool fill this query and click Run

` KubeEvents | where Namespace == "default" | where Reason == "Failed" | where Message matches regex "Failed to pull image" `
  
<img width="901" alt="image" src="https://user-images.githubusercontent.com/46469458/190915756-7cb7955b-b870-45d1-9785-464d64c7edb8.png">

11. After that click Display time (UTC+00:00) and change to Local time 

<img width="433" alt="image" src="https://user-images.githubusercontent.com/46469458/190915821-717eff64-8e40-4bf4-b74e-31eb5332b9d6.png">

12 . At query result scroll down to last record and click expand ( > ) then find messege line you will root cause 

<img width="867" alt="image" src="https://user-images.githubusercontent.com/46469458/190915985-2db6fc14-ac3e-41ae-ac83-d342ed98db85.png">

* From error in this workshop root cause is Cannot find image name "nginx:lates" (wrong image tag)

13. At left menu scroll up to Kubernetes resources and select Workloads, you will see pop-up click Ok

<img width="986" alt="image" src="https://user-images.githubusercontent.com/46469458/190916681-a8f31ee2-ce7d-4d14-93e1-f4fc14f0f22c.png">

14. At Deployments tab click on your deployment name

<img width="1084" alt="image" src="https://user-images.githubusercontent.com/46469458/190916844-31bcd8c4-a4ca-4dd2-8b54-37621080faa7.png">

15. Select YAML and scroll down to ***line number 108***

<img width="632" alt="image" src="https://user-images.githubusercontent.com/46469458/190917237-7fd8f3a4-66cd-4f9f-bfde-f080f611349c.png">

16. Change `nginx:lates` to `nginx:latest` then click Review + save

<img width="364" alt="image" src="https://user-images.githubusercontent.com/46469458/190917320-d4c633e7-ce0d-4f88-988f-30b63f354593.png">

17. Review your change and check Confirm manifest changes and click save

![image](https://user-images.githubusercontent.com/46469458/190917641-9463ffbe-19d1-49a6-b472-c1af266a81b4.png)

18. Go to top of page and click on your cluster name

![image](https://user-images.githubusercontent.com/46469458/190917740-ffafa89f-c620-4e4d-b870-4c76837b7727.png)

19. Go to Monitoring --> Insights and repeat step 4. and 5., You will see new container but status is Ok.

<img width="1182" alt="image" src="https://user-images.githubusercontent.com/46469458/190918047-751efe14-925e-4537-a166-cbd87a5d3bc1.png">

20. Click on the container ( status Ok) you will see 

  Container Status = running
  
  Container Status Reason = -

<img width="541" alt="image" src="https://user-images.githubusercontent.com/46469458/190918207-f94f5d05-b753-4180-9a20-6f5e49440db2.png">

  then switch to Live Logs tab to see real time log when incoming connection
  
<img width="1203" alt="image" src="https://user-images.githubusercontent.com/46469458/190974630-d13bd801-498d-42fc-b02b-dde7e8901513.png">

21. Workbooks 

![image](https://user-images.githubusercontent.com/46469458/190971365-46a2514f-bc88-4ac3-abab-61824b28440f.png)

<img width="1449" alt="image" src="https://user-images.githubusercontent.com/46469458/190971741-9a1310b4-dcc0-4532-abea-93348957075b.png">


