# pi5-scrypted-camera-service
A simple service to make the pi 5 camera available to scrypted. 

Only 1 client can connect to each camera. When the client disconnects, rpicam-vid for that camera restarts and re-opens the port. The intent is that scrypted will connect to the camera, and re-broadcase the stream over RTSP for use by other services. 

My current Scrypted server is a OrangePi 5 Plus running Ubuntu. The pi 5 is my 3D printer controller, and since it has no hardware h264 or encoder of any kind, 2 cameras is about the limit to still have some CPU left. The OrangePi 5 has hardware codecs which take care of further processing in Scrypted. 

camera-service opens port 8090 for camera 0 and 8091 for camera 1. The streams are 1080p at 15fps. This will use about 50% of the pi's CPU to encode these streams in h264. If you increase to 30fps, it will utilize about 80-50% CPU. 

```
sudo cp camera-service /usr/bin
sudo chown <user> /usr/bin/camera-service
sudo chmod +x /usr/bin/camera-service
sudo cp camera-service.service /etc/systemd/system/
sudo chown root /etc/systemd/system/camera-service.service
```

Edit /etc/systemd/system/camera-service.service and change User to the <user> you used above. 
