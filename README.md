# AKS-troubleshooting
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


