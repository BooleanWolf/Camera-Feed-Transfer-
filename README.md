# Camera-Feed-Transfer-

This module is designed to transmit the video feed from one device to any other device in the same network using the **HTTP protocol**. The [_server.py_](https://github.com/BooleanWolf/Camera-Feed-Transfer-/blob/master/server.py) initiates a websocket in the current network and transmits video feed from the connected camera using [_OpenCV_](https://opencv.org/). The [_client.py_](https://github.com/BooleanWolf/Camera-Feed-Transfer-/blob/master/client.py) program can be run on any device in the same network to receive the video feed from the Server.
Usually, the _server.py_ is run on the computer on the Rover ( e.g., Jetson Xavier), and the _client.py_ is run on the base station computer. This module can be used as an alternative for ROS video topics for transmitting and receiving video feeds as it can perform with lower latency.

> Note: Both server and client devices MUST BE connected to the same network, and the IP address of the server device MUST BE discoverable.

## Requirements

The module requires the following libraries installed in both client and server device:

- [opencv-python](https://pypi.org/project/opencv-python/)

## How To Use

### Server side (transmitter):

First, adjust the following parameter in the [_config.py_](https://github.com/BooleanWolf/Camera-Feed-Transfer-/blob/master/config.py) file:

- `CAMERA_INDEX`: set it to the index of the camera connected to the Server device that will be used to capture the video. (e.g., `1`)

Save the changes and run _server.py_ on the Server device. You can open a terminal in this directory and use this command in the terminal:
`python server.py`

The IP address of the Server device should now be printed in the terminal (e.g., `HOST IP: 192.168.56.1` and a video feed should be available in another window.

> NOTE: you can close the video transmission window by pressing the Q key on your keyboard.

### Client side (receiver):

On the client device, make sure that the `HOST_IP` is set accurately in the _config.py_ file.
When _server.py_ is run on the Server device, the IP address of the host should be printed on the terminal.
Open _config.py_ on the Client device and set `HOST_IP` to the IP address of the Server device (e.g., `HOST_IP= '192.168.56.1'`). Save changes and run _client.py_.
`python client.py`

Now, you should see the video feed from the Server device in a separate window.

> NOTE: you can press Q on your keyboard to close the video feed window.

**P.S.** When using the Rocket M2 for communicating between the Rover and the Base station, make sure that the network configuration is done properly and the IP address of both the Rover computer and the Base station computer are accessible, otherwise there may arise connectivity issues and the module will not work.
