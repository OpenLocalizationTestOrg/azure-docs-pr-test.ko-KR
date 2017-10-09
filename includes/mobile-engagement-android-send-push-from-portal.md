### <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a>Grant Mobile Engagement 액세스 tooyour GCM API 키
Mobile Engagement toosend 푸시 알림을 사용자 대신 tooallow 하 고, toogrant tooyour API 키에 액세스 해야 합니다. 이렇게 구성 하 고 hello Mobile Engagement 포털에 키를 입력 합니다.

1. Azure 클래식 포털에서 hello 앱에서는이 프로젝트에 대 한 사용 중이 고 hello를 클릭 한 다음에 있는 확인 **사로잡는 구성** hello 아래쪽 단추:
   
    ![](./media/mobile-engagement-android-send-push/engage-button.png)
2. Hello 클릭 **설정** -> **하 여 네이티브 푸시** tooenter GCM 키 섹션:
   
    ![](./media/mobile-engagement-android-send-push/engagement-portal.png)
3. Hello 클릭 **편집** 아이콘의 앞 **API 키** hello에 **GCM 설정** 아래와 같이 섹션:
   
    ![](./media/mobile-engagement-android-send-push/native-push-settings.png)
4. Hello 팝업에 hello 하기 전에 가져온 GCM 서버 키를 붙여 넣고 클릭 **확인**합니다.
   
    ![](./media/mobile-engagement-android-send-push/api-key.png)

## <a id="send"></a>보낼 알림 tooyour 앱
이제 푸시 알림 tooour 응용 프로그램에서 전송 하는 간단한 푸시 알림 캠페인 사항을 만듭니다.

1. Toohello 이동 **도달** Mobile engagement 연결 포털에서 탭 합니다.
2. 클릭 **새 공지** toocreate 푸시 알림 캠페인입니다.
   
    ![](./media/mobile-engagement-android-send-push/new-announcement.png)
3. 단계를 수행 하는 hello 통해 캠페인의 hello 첫 번째 필드를 설정 합니다.
   
    ![](./media/mobile-engagement-android-send-push/campaign-first-params.png)
   
    a. 캠페인 이름을 지정합니다.
   
    b. 선택 hello **배달 유형** 으로 *시스템 알림 단순->*: hello 간단한 Android 푸시 알림 형식 제목 및 텍스트 줄 작은 기능입니다.
   
    c. 선택 **배달 시간** 으로 *언제 든 지* tooallow hello 앱 tooreceive 알림을 여부 또는 not hello 응용 프로그램이 시작 됩니다.
   
    d. Hello 알림 텍스트 형식 hello에 **제목** 에 될 hello 푸시에서 굵게 표시 합니다.
   
    e. 그런 다음 **메시지**
4. 아래로 스크롤하고 hello에 **콘텐츠** 섹션에서 **알림 전용**합니다.
   
    ![](./media/mobile-engagement-android-send-push/campaign-content.png)
5. 설정을 hello 가장 기본적인 캠페인 가능한 작업이 끝났습니다. 이제 다시 아래로 스크롤하여 하 고 hello 클릭 **만들기** toosave 캠페인 단추입니다.
6. 마지막 단계: 클릭 **Activate** tooactivate 캠페인 toosend 푸시 알림에 합니다.
   
    ![](./media/mobile-engagement-android-send-push/campaign-activate.png)

