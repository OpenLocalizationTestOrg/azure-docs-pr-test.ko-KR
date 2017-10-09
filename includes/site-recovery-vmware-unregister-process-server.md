<span data-ttu-id="0447c-101">hello 단계 toounregister 프로세스 서버가 구성 서버 hello로 연결 상태에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="0447c-101">hello steps toounregister a process server differs depending on its connection status with hello Configuration Server.</span></span>

### <a name="unregister-a-process-server-that-is-in-a-connected-state"></a><span data-ttu-id="0447c-102">연결된 상태인 프로세스 서버 등록 취소</span><span class="sxs-lookup"><span data-stu-id="0447c-102">Unregister a process server that is in a connected state</span></span>

1. <span data-ttu-id="0447c-103">원격 관리자 권한으로 프로세스 서버 hello로 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="0447c-103">Remote into hello process server as an Administrator.</span></span>
2. <span data-ttu-id="0447c-104">Hello 시작 **제어판** 엽니다 **프로그램 > 프로그램 제거**</span><span class="sxs-lookup"><span data-stu-id="0447c-104">Launch hello **Control Panel** and open **Programs > Uninstall a program**</span></span>
3. <span data-ttu-id="0447c-105">Hello 이름별 프로그램 제거 **Microsoft Azure 사이트 복구 구성/프로세스 서버**</span><span class="sxs-lookup"><span data-stu-id="0447c-105">Uninstall a program by hello name **Microsoft Azure Site Recovery Configuration/Process Server**</span></span>
4. <span data-ttu-id="0447c-106">3단계가 완료되면 **Microsoft Azure Site Recovery 구성/프로세스 서버**를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0447c-106">Once step 3 is completed, you can uninstall **Microsoft Azure Site Recovery Configuration/Process Server Dependencies**</span></span>

### <a name="unregister-a-process-server-that-is-in-a-disconnected-state"></a><span data-ttu-id="0447c-107">연결 해제된 상태인 프로세스 서버 등록 취소</span><span class="sxs-lookup"><span data-stu-id="0447c-107">Unregister a process server that is in a disconnected state</span></span>

> [!WARNING]
> <span data-ttu-id="0447c-108">프로세스 서버가 설치 되어 있는 hello 없는 방식으로 toorevive hello 가상 컴퓨터인 경우 아래 단계에 사용 하 여 hello는 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0447c-108">Use hello below steps should be used if there is no way toorevive hello virtual machine on which hello Process Server was installed.</span></span>

1. <span data-ttu-id="0447c-109">관리자 권한으로 tooyour 구성 서버에 로그온 합니다.</span><span class="sxs-lookup"><span data-stu-id="0447c-109">Log on tooyour configuration server as an Administrator.</span></span>
2. <span data-ttu-id="0447c-110">관리 명령 프롬프트를 열고 toohello 디렉터리 찾아보기 `%ProgramData%\ASR\home\svsystems\bin`합니다.</span><span class="sxs-lookup"><span data-stu-id="0447c-110">Open an Administrative command prompt and browse toohello directory `%ProgramData%\ASR\home\svsystems\bin`.</span></span>
3. <span data-ttu-id="0447c-111">이제 hello 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0447c-111">Now run hello command.</span></span>

    ```
    perl Unregister-ASRComponent.pl -IPAddress <IP_of_Process_Server> -Component PS
    ```
4. <span data-ttu-id="0447c-112">Hello 프로세스 서버 hello 세부 정보를 제거할이 hello 시스템에서 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0447c-112">This will purge hello details of hello process server from hello system.</span></span>
