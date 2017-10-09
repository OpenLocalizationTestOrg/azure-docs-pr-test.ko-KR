> [!IMPORTANT]
> <span data-ttu-id="83f90-101">Mobile Engagement에서 푸시 알림을 tooreceive 해야 tooenable `Silent Remote Notifications` 응용 프로그램에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="83f90-101">tooreceive Push Notifications from Mobile Engagement, you need tooenable `Silent Remote Notifications` in your application.</span></span> <span data-ttu-id="83f90-102">Info.plist 파일에 tooadd hello 원격 알림 값 toohello UIBackgroundModes 배열을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="83f90-102">You need tooadd hello remote-notification value toohello UIBackgroundModes array in your Info.plist file.</span></span>
> 
> 

1. <span data-ttu-id="83f90-103">열기 `info.plist` hello 프로젝트의 파일</span><span class="sxs-lookup"><span data-stu-id="83f90-103">Open `info.plist` file in hello project</span></span>
2. <span data-ttu-id="83f90-104">Hello 목록의 hello 상위 항목을 마우스 오른쪽 단추로 클릭 (`Information Property List`) 및 새 행 추가</span><span class="sxs-lookup"><span data-stu-id="83f90-104">Right click on hello top item in hello list (`Information Property List`) and add a new row</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push1.png)
3. <span data-ttu-id="83f90-105">Hello 새 행에 입력`Required background modes`</span><span class="sxs-lookup"><span data-stu-id="83f90-105">In hello new row enter `Required background modes`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push2.png)
4. <span data-ttu-id="83f90-106">Hello 왼쪽된 화살표 tooexpand hello 행을 클릭</span><span class="sxs-lookup"><span data-stu-id="83f90-106">Click on hello left arrow tooexpand hello row</span></span>
5. <span data-ttu-id="83f90-107">Hello 0 값 toohello 항목 뒤에 추가 합니다.`App downloads content in response toopush notifications`</span><span class="sxs-lookup"><span data-stu-id="83f90-107">Add hello following value toohello item 0 `App downloads content in response toopush notifications`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push3.png)
6. <span data-ttu-id="83f90-108">Hello 변경 하면 XML hello 다음을 포함 해야 하는 hello info.plist 키와 값:</span><span class="sxs-lookup"><span data-stu-id="83f90-108">Once you make hello change, hello info.plist XML should contain hello following key and value:</span></span>
   
        <key>UIBackgroundModes</key>
        <array>
        <string>remote-notification</string>
        </array>
7. <span data-ttu-id="83f90-109">**Xcode 7+** 및**iOS 9+**를 사용 중인 경우,</span><span class="sxs-lookup"><span data-stu-id="83f90-109">If you are using **Xcode 7+** and **iOS 9+**:</span></span>
   
   * <span data-ttu-id="83f90-110">대상 > 대상 이름 > 기능에서 **푸시 알림**을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="83f90-110">Enable **Push Notifications** in Targets > Your Target Name > Capabilities.</span></span>

