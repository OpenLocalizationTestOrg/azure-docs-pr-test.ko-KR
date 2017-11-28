<span data-ttu-id="5260a-101">프로세스 서버를 등록 취소하는 단계는 구성 서버와의 연결 상태에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="5260a-101">The steps to unregister a process server differs depending on its connection status with the Configuration Server.</span></span>

### <a name="unregister-a-process-server-that-is-in-a-connected-state"></a><span data-ttu-id="5260a-102">연결된 상태인 프로세스 서버 등록 취소</span><span class="sxs-lookup"><span data-stu-id="5260a-102">Unregister a process server that is in a connected state</span></span>

1. <span data-ttu-id="5260a-103">관리자 권한으로 프로세스 서버에 원격 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5260a-103">Remote into the process server as an Administrator.</span></span>
2. <span data-ttu-id="5260a-104">**제어판**을 실행하고 **프로그램 > 프로그램 제거**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5260a-104">Launch the **Control Panel** and open **Programs > Uninstall a program**</span></span>
3. <span data-ttu-id="5260a-105">Uninstall a program by the name **Microsoft Azure Site Recovery 구성/프로세스 서버** 이름으로 프로그램을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="5260a-105">Uninstall a program by the name **Microsoft Azure Site Recovery Configuration/Process Server**</span></span>
4. <span data-ttu-id="5260a-106">3단계가 완료되면 **Microsoft Azure Site Recovery 구성/프로세스 서버**를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260a-106">Once step 3 is completed, you can uninstall **Microsoft Azure Site Recovery Configuration/Process Server Dependencies**</span></span>

### <a name="unregister-a-process-server-that-is-in-a-disconnected-state"></a><span data-ttu-id="5260a-107">연결 해제된 상태인 프로세스 서버 등록 취소</span><span class="sxs-lookup"><span data-stu-id="5260a-107">Unregister a process server that is in a disconnected state</span></span>

> [!WARNING]
> <span data-ttu-id="5260a-108">아래 단계는 프로세스 서버가 설치된 가상 컴퓨터를 복구할 방법이 없는 경우 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5260a-108">Use the below steps should be used if there is no way to revive the virtual machine on which the Process Server was installed.</span></span>

1. <span data-ttu-id="5260a-109">관리자 권한으로 구성 서버에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="5260a-109">Log on to your configuration server as an Administrator.</span></span>
2. <span data-ttu-id="5260a-110">관리 명령 프롬프트를 열고 `%ProgramData%\ASR\home\svsystems\bin` 디렉터리를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5260a-110">Open an Administrative command prompt and browse to the directory `%ProgramData%\ASR\home\svsystems\bin`.</span></span>
3. <span data-ttu-id="5260a-111">이제 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5260a-111">Now run the command.</span></span>

    ```
    perl Unregister-ASRComponent.pl -IPAddress <IP_of_Process_Server> -Component PS
    ```
4. <span data-ttu-id="5260a-112">그러면 시스템에서 프로세스 서버의 세부 정보를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="5260a-112">This will purge the details of the process server from the system.</span></span>
