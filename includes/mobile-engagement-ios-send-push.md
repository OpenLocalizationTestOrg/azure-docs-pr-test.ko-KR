### <a name="grant-access-tooyour-push-certificate-toomobile-engagement"></a>권한 부여 액세스 tooyour 푸시 인증서 tooMobile Engagement
사용자 대신 tooallow Mobile Engagement toosend 푸시 알림을, toogrant tooyour 인증서에 액세스 해야 합니다. 이렇게 구성 하 고 hello Mobile Engagement 포털에 인증서를 입력 합니다. [Apple 설명서](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)

1. Mobile engagement 연결 포털 tooyour 이동 합니다. 확인 올바른 hello에 있는 한 hello에서 클릭 한 다음 **사로잡는 구성** hello 아래쪽 단추:
   
    ![](./media/mobile-engagement-ios-send-push/engage-button.png)
2. Hello 클릭 **설정을** engagement 연결 포털에서 페이지입니다. Hello 없어 클릭에서 **하 여 네이티브 푸시** tooupload p12 인증서 섹션:
   
    ![](./media/mobile-engagement-ios-send-push/engagement-portal.png)
3. 다음과 같이 p12를 선택하여 업로드하고 암호를 입력합니다.
   
    ![](./media/mobile-engagement-ios-send-push/native-push-settings.png)

## <a id="send"></a>보낼 알림 tooyour 앱
이제 푸시 tooour 앱 보낼 단순한 푸시 알림을 캠페인 사항을 만듭니다.

1. Toohello 이동 **도달** Mobile engagement 연결 포털에서 탭 합니다.
2. 클릭 **새 공지** toocreate 푸시 캠페인
   
    ![](./media/mobile-engagement-ios-send-push/new-announcement.png)
3. 캠페인의 첫 번째 필드 hello 설치:
   
    ![](./media/mobile-engagement-ios-send-push/campaign-first-params.png)
   
   * 캠페인 **이름** 을 입력합니다. 
   * 선택 hello **배달 시간** 으로 **앱 외부만**: 일부 텍스트 옵션이 있는 hello 간단한 Apple 푸시 알림 유형입니다.
   * Hello 알림 텍스트에서 첫 번째 hello 입력 **제목** 를 hello hello 푸시에서 첫 번째 줄 수 있습니다.
   * 입력 한 다음 프로그램 **메시지** hello 두 번째 줄 됩니다
4. Hello에서 콘텐츠 섹션을 선택 하 고 아래로 스크롤하여 **알림 전용**
   
    ![](./media/mobile-engagement-ios-send-push/campaign-content.png)
5. 설정을 hello 가장 기본적인 캠페인을 완료 것입니다. 이제 아래로 스크롤하여 클릭 **만들기** toosave 푸시 알림 캠페인 단추입니다. 
6. 마지막으로-클릭 **Activate** toosend 푸시 알림입니다. 
   
    ![](./media/mobile-engagement-ios-send-push/campaign-activate.png)
7. 수 없게 됩니다. hello 다음과 같은 hello 알림 센터에 iOS 장치에서 hello 알림을 수신 합니다.
   
    ![](./media/mobile-engagement-ios-send-push/iphone-notification.png)
8. 이 iOS 장치를 함께 사용 하는 Apple Watch 있으면 hello 알림을 Apple Watch 볼 수 있습니다.
   
    ![](./media/mobile-engagement-ios-send-push/apple-watch.png)

