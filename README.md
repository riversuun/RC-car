# RC-car
sudo: "superuser do"의 약자로, 사용자가 슈퍼 사용자 권한을 사용하여 다른 명령어나 스크립트를 실행하도록 허용하는 데 사용됩니다. 슈퍼 사용자 권한은 시스템 전체에 대한 권한을 부여하며 주의해서 사용해야 합니다.

sh: 쉘 명령어를 실행하는 프로그램입니다. sh는 기본 쉘로서, 쉘 스크립트나 명령어를 실행하는 역할을 합니다.

install.sh: 스크립트 파일의 이름입니다. 이 명령어는 스크립트 파일인 install.sh를 실행하려는 것입니다.

wifi
$ sudo nmcli device wifi list
$ sudo nmcli device wifi connect <ssid_name> password <password>
$ ifconfig

연결해제 : $ sudo nmcli device disconnect wlan0

2장, Jetpack & ROS install

https://drive.google.com/file/d/1HU5F1cwiw2wzuNBdLL9R3Wvpg5AXLzw5/view?usp=sharing

1.2 Cooling Fan
cd Downloads
git clone https://github.com/jetsonworld/jetson-fan-ctl.git
cd jetson-fan-ctl

sudo sh install.sh
![Screenshot from 2023-11-01 18-46-20](https://github.com/riversuun/RC-car/assets/128311480/10a2ff05-5cb5-4897-a754-d822f7576dcb)

2.1 ROS Melodic 설치

cd ~/Downloads/
sudo apt update

git clone https://github.com/zeta0707/installROS.git
cd installROS
./install-ros.sh

2.2 .bashrc 수정
주석 처리는 필수로 해야합니다

Control Your Robot!
---------------------------
Moving around:
        w
   a    s    d
        x

w/x : increase/decrease linear velocity (~ 1.2 m/s)
a/d : increase/decrease angular velocity (~ 1.8)

space key, s : force stop

CTRL-C to quit


terminal #1
$ roslaunch jessicar_control keyboard_control.launch

terminal #2
$ roslaunch jessicar_teleop jessicar_teleop_key.launch

gst-launch로 확인(Option) camera orientation을 맞게 설정해야합니다. flip-method=0이 jetracer에게 맞는 방향입니다만 camera install에 따라 값을 0 또는 1로 변경해주세요. gst-launch-1.0 nvarguscamerasrc sensor_id=0 ! 'video/x-raw(memory:NVMM),width=3280, height=2464, framerate=21/1, format=NV12' ! nvvidconv flip-method=0 ! 'video/x-raw,width=960, height=720' ! nvvidconv ! nvegltransform ! nveglglessink -e

csi_pub.py으로 확인 Jetson CSI camera를 image_view package를 통해 camera가 잘 동작하는지 확인합니다. 
$ sudo apt install ros-melodic-image-view​



