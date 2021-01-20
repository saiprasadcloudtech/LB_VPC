# Project Description
In this project, I will try to create a video streaming website. ALl the resources will be inside a VPC and the only way to access them is through Load balancer. I will try to incorporate path based routing with 2 web pages( home page and a video streaming page ). This will be an added security feature to the resources within VPC. I will also try to include Route 53 and access the webpages through a free domain.

Step 1 : Create a VPC with 2 private subnets in different AZ's for resilence purpose

step 2 : create 2 public subnets in different AZ's 
Step 3: create Internet gateway

step 4: create 2 route tables - internet route route table and a non internet route table

step 5 : add subnets to the respective route tables and also edit route for each route table to get internet connection.

step 6 : create a ubuntu web server  in the public subnet 

step 7 : login to the server and do the following update
         $sudo apt get-update     # update the server
         $sudo apt get-install apache2         # install apache to make it as web server
         
step 8 : create a html page inside /var/www/html   #index.html page 

step 9 : create an image from the ec2 instance and use the image to create  ubuntu servers in private subnets (for home page)

step 10 : repeat step 8 with a different html file and create another image from ec2 instance. using this image create another server in private subnet (for streamin     
          page )
          
step 11: only way to login to private servers is through the public server and there is no other way. 

step 12: To login first copy the pem file into the public server (/home/ubuntu) and run the below command 
          $ ssh -i ./<pem file name> ubuntu@<private_server_ip>
         
step 13: configure application load balancer to implement path based routing # it supports only http protocol

step 14: create target group for a home page server and another target group for streaming page server

step 15: once load balancer is created , edit rules under listener   

step 16 : Insert rule for both the servers ( home and streaming server )   # (set path to /home* and /watch* and forward to respective server )

step 17 : access the home page using the the DNS name of the load balancer

step 18 : but stremaing page may not work ( DNS/watch ) because we need to add a folder inside (/var/www/html )

step 19 : login to both server and create a directory called watch and home inside the /var/www/html
          $sudo cp ./index.html ./watch/        $sudo cp ./index.html ./home/ 
         
step 20: create a free domain from freenom website 

step 21: create hosted zone under route 53 . enter the domain name which we just created 

step 22: copy the name servers and paste in into freenom dashboard . this will connect my domain to the route53 

step 23: create record set in route 53 and point the route 53 to load balancer 
                * select alias and select your load balancer as alias target 
                
step 24 : create another record set with www entered as a prefix for the record name 
                  * select alias and select your load balancer as alias target
                  
step 25 : Try accessing the home page using the domain name and will work . similarly try with /watch and it should open the streaming page 


        
