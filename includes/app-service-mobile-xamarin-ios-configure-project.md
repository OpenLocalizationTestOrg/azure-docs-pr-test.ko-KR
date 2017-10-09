#### <a name="configure-hello-ios-project-in-xamarin-studio"></a>Xamarin Studio에서 hello iOS 프로젝트를 구성 합니다.
1. Xamarin.Studio를 열고 **Info.plist**, 및 업데이트 hello **번들 식별자** hello로 새 앱 ID를 사용 하 여 이전에 만든 ID 번들

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-21.png)
2. 너무 아래로 스크롤하여**백그라운드 모드**합니다. 선택 hello **백그라운드 모드를 사용 하도록 설정** 상자와 hello **원격 알림** 상자입니다.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-22.png)
3. Hello 솔루션 패널 tooopen에서 프로젝트를 두 번 클릭 **프로젝트 옵션**합니다.
4. 아래 **빌드**, 선택 **iOS 번들 서명**, 선택 hello 해당 id 및 프로비저닝 프로필 방금 설정한이 프로젝트에 대 한 합니다.

   ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-20.png)

   이렇게 하면 해당 hello 프로젝트 코드 서명에 hello 새 프로필을 사용 합니다. Hello Xamarin 장치 공식 설명서를 프로 비전에 대 한 참조 [Xamarin 장치 프로 비전]합니다.

#### <a name="configure-hello-ios-project-in-visual-studio"></a>Visual Studio에서 hello iOS 프로젝트를 구성 합니다.
1. Visual Studio에서 hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성**합니다.
2. Hello 속성 페이지에서 클릭 hello **iOS 응용 프로그램** 탭 및 업데이트 hello **식별자** 앞에서 만든 hello id입니다.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-23.png)
3. Hello에 **iOS 번들 서명** 탭을 선택 하는 hello 해당 id 및 프로비저닝 프로필 ड ि를이 프로젝트에 대 한 합니다.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-24.png)

    이렇게 하면 해당 hello 프로젝트 코드 서명에 hello 새 프로필을 사용 합니다. Hello Xamarin 장치 공식 설명서를 프로 비전에 대 한 참조 [Xamarin 장치 프로 비전]합니다.
4. Info.plist tooopen를 두 번 클릭 한 다음 사용 **RemoteNotifications** 아래 **백그라운드 모드**합니다.

[Xamarin 장치 프로 비전]: http://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning/
