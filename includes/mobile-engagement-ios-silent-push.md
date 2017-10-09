> [!IMPORTANT]
> Mobile Engagement에서 푸시 알림을 tooreceive 해야 tooenable `Silent Remote Notifications` 응용 프로그램에서 합니다. Info.plist 파일에 tooadd hello 원격 알림 값 toohello UIBackgroundModes 배열을 해야합니다.
> 
> 

1. 열기 `info.plist` hello 프로젝트의 파일
2. Hello 목록의 hello 상위 항목을 마우스 오른쪽 단추로 클릭 (`Information Property List`) 및 새 행 추가
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push1.png)
3. Hello 새 행에 입력`Required background modes`
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push2.png)
4. Hello 왼쪽된 화살표 tooexpand hello 행을 클릭
5. Hello 0 값 toohello 항목 뒤에 추가 합니다.`App downloads content in response toopush notifications`
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push3.png)
6. Hello 변경 하면 XML hello 다음을 포함 해야 하는 hello info.plist 키와 값:
   
        <key>UIBackgroundModes</key>
        <array>
        <string>remote-notification</string>
        </array>
7. **Xcode 7+** 및**iOS 9+**를 사용 중인 경우,
   
   * 대상 > 대상 이름 > 기능에서 **푸시 알림**을 사용하도록 설정합니다.

