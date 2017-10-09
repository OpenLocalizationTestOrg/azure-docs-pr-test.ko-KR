
1. <span data-ttu-id="e4423-101">솔루션 뷰 hello에 (또는 **솔루션 탐색기** Visual Studio에서)를 마우스 오른쪽 단추로 클릭 hello **구성 요소** 폴더를 클릭 **더 구성 요소 가져오기...** , hello에 대 한 검색 **Google 클라우드 메시징 클라이언트** 구성 요소 toohello 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4423-101">In hello Solution view (or **Solution Explorer** in Visual Studio), right-click hello **Components** folder, click  **Get More Components...**, search for hello **Google Cloud Messaging Client** component and add it toohello project.</span></span>
2. <span data-ttu-id="e4423-102">Hello ToDoActivity.cs 프로젝트 파일을 열고 hello 다음 추가 문 toohello 클래스를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="e4423-102">Open hello ToDoActivity.cs project file and add hello following using statement toohello class:</span></span>
   
        using Gcm.Client;
3. <span data-ttu-id="e4423-103">Hello에 **ToDoActivity** 클래스 hello 다음 새 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4423-103">In hello **ToDoActivity** class, add hello following new code:</span></span> 
   
        // Create a new instance field for this activity.
        static ToDoActivity instance = new ToDoActivity();
   
        // Return hello current activity instance.
        public static ToDoActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }
        // Return hello Mobile Services client.
        public MobileServiceClient CurrentClient
        {
            get
            {
                return client;
            }
        }
   
    <span data-ttu-id="e4423-104">이렇게 하면 hello 푸시 처리기 서비스 프로세스에서 tooaccess hello 모바일 클라이언트 인스턴스 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4423-104">This enables you tooaccess hello mobile client instance from hello push handler service process.</span></span>
4. <span data-ttu-id="e4423-105">Hello 코드 toohello 다음 추가 **OnCreate** 메서드 hello 후 **MobileServiceClient** 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="e4423-105">Add hello following code toohello **OnCreate** method, after hello **MobileServiceClient** is created:</span></span>
   
       // Set hello current instance of TodoActivity.
       instance = this;
   
       // Make sure hello GCM client is set up correctly.
       GcmClient.CheckDevice(this);
       GcmClient.CheckManifest(this);
   
       // Register hello app for push notifications.
       GcmClient.Register(this, ToDoBroadcastReceiver.senderIDs);

<span data-ttu-id="e4423-106">이제 **ToDoActivity** 이 푸시 알림 추가를 위해 준비됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4423-106">Your **ToDoActivity** is now prepared for adding push notifications.</span></span>

