
1. Visual Studio 솔루션 탐색기에서 hello Windows 스토어 앱 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **저장소** > **hello 저장소로 응용 프로그램 연결**합니다.

    ![Windows 스토어에 응용 프로그램 연결](./media/app-service-mobile-register-wns/notification-hub-associate-win8-app.png)
2. Hello 마법사에서 **다음**, Microsoft 계정으로 로그인 합니다. **새 앱 이름 예약**에 앱의 이름을 입력한 후 **예약**을 클릭합니다.
3. Hello 앱 등록을 성공적으로 만든 hello 새로운 앱 이름 되 면 클릭 **다음**, 클릭 하 고 **연결**합니다. 이 hello 필요한 Windows 스토어 등록 정보 toohello 응용 프로그램 매니페스트를 추가합니다.
4. 사용 하 여 1 및 Windows Phone 스토어 앱 프로젝트 hello에 대 한 3 단계를 반복 하 여 hello hello Windows 스토어 앱에 대해 이전에 만든 동일한 등록 합니다.  
5. Toohello 찾아보기 [Windows 개발자 센터](https://dev.windows.com/en-us/overview), Microsoft 계정으로 로그인 합니다. 에 새 응용 프로그램 등록 hello 클릭 **My apps**, 펼친 다음 **서비스** > **푸시 알림**합니다.
6. Hello에 **푸시 알림** 페이지 **Live 서비스 사이트** 아래 **WNS Windows 푸시 알림 서비스 () 및 Microsoft Azure 모바일 앱**합니다. Hello의 hello 값 메모 **패키지 SID** 및 hello *현재* 값 **응용 프로그램 암호**합니다. 

    ![Hello 개발자 센터의 응용 프로그램 설정](./media/app-service-mobile-register-wns/mobile-services-win8-app-push-auth.png)

   > [!IMPORTANT]
   > hello 응용 프로그램 암호와 패키지 SID는 중요 한 보안 자격 증명. 다른 사람과 공유하지 말고 앱과 함께 분산하지 마세요.
   >
   >
