# Try to run it

1. start server

``
nohup java -Dlog4j.configuration=file:../config/log4j.properties -cp ambry.jar com.github.ambry.server.AmbryMain --serverPropsFilePath ../config/server.properties --hardwareLayoutFilePath ../config/HardwareLayout.json --partitionLayoutFilePath ../config/PartitionLayout.json > logs/server.log &
``

2. start fronted
``
nohup java -Dlog4j.configuration=file:../config/log4j.properties -cp ambry.jar com.github.ambry.frontend.AmbryFrontendMain --serverPropsFilePath ../config/frontend.properties --hardwareLayoutFilePath ../config/HardwareLayout.json --partitionLayoutFilePath ../config/PartitionLayout.json > logs/frontend.log &
``

3. post image
``
zpro:target zilla$ curl -i -H "x-ambry-service-id : CUrlUpload"  -H "x-ambry-owner-id : `whoami`" -H "x-ambry-content-type : image/gif" -H "x-ambry-um-description : Demonstration Image" http://localhost:1174/ --data-binary @demo.png
HTTP/1.1 201 Created
Location: /AAIAAf__AAAAAQAAAAAAAAAAAAAAJGEyNzA0MzU1LTM4ZmUtNGVkYy05NmM5LWQ1YmM5OWVmYTkxYg
Date: Mon, 06 Nov 2017 04:12:17 GMT
Content-Length: 0
x-ambry-creation-time: Mon, 06 Nov 2017 04:12:15 GMT
``

4. get info
``
curl -i http://localhost:1174/AAIAAf__AAAAAQAAAAAAAAAAAAAAJGEyNzA0MzU1LTM4ZmUtNGVkYy05NmM5LWQ1YmM5OWVmYTkxYg/BlobInfo
``
5. download
``
curl http://localhost:1174/AAIAAf__AAAAAQAAAAAAAAAAAAAAJGEyNzA0MzU1LTM4ZmUtNGVkYy05NmM5LWQ1YmM5OWVmYTkxYg > demo-downloaded.png
``
6. (optional)diff images.
``
diff demo.png demo-downloaded.png 
``


