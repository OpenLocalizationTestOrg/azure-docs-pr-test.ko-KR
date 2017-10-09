
1. Toohello 이동 [Google 클라우드 콘솔](https://console.developers.google.com/project), Google 계정 자격 증명을 사용 하 여 로그인 합니다. 
2. **프로젝트 만들기**를 클릭하고 프로젝트 이름을 입력한 후에 **만들기**를 클릭합니다. 요청 된 경우 hello SMS 확인을 수행 하 고 클릭 **만들기** 다시 합니다.
   
    ![새 프로젝트 만들기](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-new-project.png)   
   
     새 **프로젝트 이름**을 입력하고 **프로젝트 만들기**를 클릭합니다.
3. Hello 클릭 **유틸리티 등** 단추를 선택한 다음 클릭 **프로젝트 정보**합니다. Hello 메모 **프로젝트 번호**합니다. Tooset hello로이 값이 필요한 합니다 `SenderId` hello 클라이언트 앱에서 변수입니다.
   
    ![유틸리티 및 기타 정보](./media/mobile-services-enable-google-cloud-messaging/notification-hubs-utilities-and-more.png)
4. Hello, 대시보드를 아래에서 프로젝트 **모바일 Api**, 클릭 **Google Cloud Messaging**, hello 다음 페이지에서 클릭 **API 사용** hello 서비스 약관에 동의 하 고 합니다. 
   
    ![GCM 사용 설정](./media/mobile-services-enable-google-cloud-messaging/enable-GCM.png)
   
    ![GCM 사용 설정](./media/mobile-services-enable-google-cloud-messaging/enable-gcm-2.png) 
5. Hello 프로젝트 대시보드 클릭 **자격 증명** > **Create Credential** > **API 키**합니다. 
   
    ![](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-create-server-key.png)
6. **새 키 만들기**에서 **서버 키**를 클릭하고 사용자의 키에 대한 이름을 입력한 다음 **만들기**를 클릭합니다.
7. Hello 메모 **API 키** 값입니다.
   
    이 API 키 값 tooenable Azure tooauthenticate GCM과 함께 사용 되 고 응용 프로그램을 대신 하 여 푸시 알림을 보낼 됩니다.

