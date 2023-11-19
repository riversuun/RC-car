# RC-car
sudo: "superuser do"의 약자로, 사용자가 슈퍼 사용자 권한을 사용하여 다른 명령어나 스크립트를 실행하도록 허용하는 데 사용됩니다. 슈퍼 사용자 권한은 시스템 전체에 대한 권한을 부여하며 주의해서 사용해야 합니다.

sh: 쉘 명령어를 실행하는 프로그램입니다. sh는 기본 쉘로서, 쉘 스크립트나 명령어를 실행하는 역할을 합니다.

install.sh: 스크립트 파일의 이름입니다. 이 명령어는 스크립트 파일인 install.sh를 실행하려는 것입니다.
"ROS Melodic"은 "Robot Operating System Melodic Morenia"의 약자입니다. ROS는 로봇 및 자율 주행 시스템 개발을 위한 오픈 소스 로봇 소프트웨어 플랫폼입니다. "Melodic"은 ROS의 버전 이름으로, 각 버전은 알파벳 순서대로 이름을 붙입니다.

"Melodic Morenia"은 2018년에 릴리스된 ROS의 버전으로, 그 이전 버전인 "Kinetic Kame" 이후에 나온 것입니다. ROS Melodic은 주로 우분투 18.04 LTS 기반에서 작동하며, 로봇 개발 및 제어에 필요한 라이브러리, 도구, 패키지 및 프레임워크를 제공합니다.

ROS는 각종 센서, 액추에이터, 로봇 하드웨어와 통합하여 로봇 시스템을 구축하고 프로그래밍하는 데 사용됩니다. ROS는 로봇 개발 및 연구를 위한 표준 플랫폼으로 널리 사용되며 로봇 제어, 컴퓨터 비전, SLAM (Simultaneous Localization and Mapping), 인공 지능 등의 분야에서 활용됩니다. "Melodic"은 ROS의 중요한 버전 중 하나이며, 로봇 관련 프로젝트 및 연구를 수행하는 데 유용한 도구를 제공합니다.
"cca"와 "cma"는 보통 리눅스 터미널에서 실행되는 명령어가 아닌 것으로 보입니다. 일반적으로 리눅스 명령어는 터미널에서 사용자가 컴퓨터에 대한 명령을 내리기 위해 입력합니다.

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
192.168.55.1: Jetson IP
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

