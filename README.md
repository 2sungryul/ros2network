# ros2network
ros2 network configuration


# How to configure bridged networking mode for WSL2
1. 윈도우즈 검색창에 그룹정책편집 검색 또는 gpedit.msc 입력후 엔터

![image](https://github.com/user-attachments/assets/c7f1d5c6-77e4-46f4-b082-926672a985be)

2. 좌측창 -> 컴퓨터구성 -> 관리템플릿 -> 네트워크 -> Windows 연결관리자 -> 인터넷 또는 Windows 도메인에 대한 동시 연결수 최소화 -> 좌측 0 = 동시연결허용 설정 -> 확인

![image](https://github.com/user-attachments/assets/d58a6961-d2fb-4e98-accf-e1dfc3dd0aa5)

3. 윈도우즈 검색창에 hyper-v 관리자 검색 후 엔터

![image](https://github.com/user-attachments/assets/fab0310a-f988-4904-8adf-fc8c2ac67cc5)

4. 우측창의 가상스위치 관리자 클릭 -> 우측 가상스위치만들기 클릭

![image](https://github.com/user-attachments/assets/34540f5f-4f7b-4b19-8abc-13bf45af9ee2)

5. 가상스위치 만들기 메뉴에서 -> 이름 external, 연결형식은 외부 네트워크, 연결할 무선랜카드선택, 나머지는 선택하지 말것 -> 확인

![image](https://github.com/user-attachments/assets/838af903-03d3-49e9-9e54-7b42a6e024df)

6. 윈도우즈 설정 -> 네트워크 및 인터넷 -> 네트워크 브리지 생성 확인

![image](https://github.com/user-attachments/assets/95349d22-86b4-4ecd-92a0-5fe1e8700afe)

7. 윈도우즈 폴더 C:\Users\\<사용자id> 아래에 .wslconfig 이름의 텍스트 파일생성(확장자없어야함), 내용은 메모장열고 아래처럼 작성

```bash
[WSL2]
#networkingMode = mirrored
networkingMode = bridged
vmSwitch = external
```

![image](https://github.com/user-attachments/assets/81bddf53-3865-404c-b0a2-6700988e8177)

![image](https://github.com/user-attachments/assets/600b1e19-99b6-4458-91ff-b26079700a7f)

브리지모드로 설정하면 모든 컴퓨터의 wsl2에서 ip주소가 동일하다. 서로다른 ip를 갖도록 하려면 mac 주소를 강제로 변경해주면 된다. 아래문장을 .wslconfig파일에 추가해주면됨

```bash
[WSL2]
#networkingMode = mirrored
networkingMode = bridged
vmSwitch = external
macAddress=00:11:22:33:44:55
```

8. .wslconfig 파일내용을 수정하면 반드시 wsl2를 shutdown후 다시 실행해야함

<img width="712" height="234" alt="image" src="https://github.com/user-attachments/assets/24b7f0bd-ead7-449a-9628-cae134b42ab8" />

9. wsl2-ubuntu20.04 실행하고 ifconfig 명령실행하면 192.168.0.x 형식의 ip주소가 할당되어야 함 -> wsl2가 무선공유기에 직접 연결되었음을 의미

![image](https://github.com/user-attachments/assets/650ee692-d441-4e2d-a689-4e305a2827a4)

# How to configure mirrored networking mode for WSL2

mirrored networking modes는 wsl2가 windows와 네트워크를 공유하는 설정임 -> wsl2과 windows가 동일한 ip주소를 가짐
mirrored networking mode 사용시에는 .wslconfig 파일의 내용을 다음처럼 수정 후 wsl2를 shutdown후 다시 실행해야함

```bash
[WSL2]
networkingMode=mirrored
```


