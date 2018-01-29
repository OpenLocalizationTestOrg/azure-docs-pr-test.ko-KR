

1. [Firebase 콘솔](https://firebase.google.com/console/)에 로그인합니다. 아직 없는 경우 새 Firebase 프로젝트를 만듭니다.
2. 프로젝트를 만든 후에 **Android 앱에 Firebase 추가**를 클릭하고 제공된 지침을 따릅니다.

    ![](./media/notification-hubs-enable-firebase-cloud-messaging/notification-hubs-add-firebase-to-android-app.png)
3. Firebase 콘솔에서 프로젝트에 대한 톱니바퀴를 클릭한 다음 **프로젝트 설정**을 클릭합니다.

    ![](./media/notification-hubs-enable-firebase-cloud-messaging/notification-hubs-firebase-console-project-settings.png)
4. 프로젝트 설정에서 **일반** 탭을 클릭한 다음, 서버 API 키와 클라이언트 ID가 포함된 **google-services.json** 파일을 다운로드합니다.
5. 프로젝트 설정에서 **클라우드 메시지** 탭을 클릭하고, **레거시 서버 키**의 값을 복사합니다. 이 값은 알림 허브 액세스 정책을 구성하는 데 사용됩니다.
