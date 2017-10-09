<!--author=SharS last changed: 9/17/15-->

#### <a name="tooconnect-through-hello-serial-console"></a><span data-ttu-id="27098-101">hello 직렬 콘솔을 통해 tooconnect</span><span class="sxs-lookup"><span data-stu-id="27098-101">tooconnect through hello serial console</span></span>
1. <span data-ttu-id="27098-102">직렬 케이블 toohello 장치 (직접 또는 USB 직렬 어댑터를 통해)에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="27098-102">Connect your serial cable toohello device (directly or through a USB-serial adapter).</span></span>
2. <span data-ttu-id="27098-103">열기 hello **제어판**를 연 다음 hello **장치 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="27098-103">Open hello **Control Panel**, and then open hello **Device Manager**.</span></span>
3. <span data-ttu-id="27098-104">Hello 다음 그림에에서 표시 된 대로 hello COM 포트를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="27098-104">Identify hello COM port as shown in hello following illustration.</span></span>
   
     ![직렬 콘솔을 통해 연결](./media/storsimple-use-putty/HCS_ConnectingDeviceS-include.png)
4. <span data-ttu-id="27098-106">PuTTY를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="27098-106">Start PuTTY.</span></span> 
5. <span data-ttu-id="27098-107">Hello 오른쪽 창에서 변경 hello **연결 유형** 너무**직렬**합니다.</span><span class="sxs-lookup"><span data-stu-id="27098-107">In hello right pane, change hello **Connection type** too**Serial**.</span></span>
6. <span data-ttu-id="27098-108">Hello 오른쪽 창에서 hello 적절 한 COM 포트를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="27098-108">In hello right pane, type hello appropriate COM port.</span></span> <span data-ttu-id="27098-109">Hello 직렬 구성 매개 변수가 다음과 같이 설정 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="27098-109">Make sure that hello serial configuration parameters are set as follows:</span></span>
   
   * <span data-ttu-id="27098-110">속도: 115,200</span><span class="sxs-lookup"><span data-stu-id="27098-110">Speed: 115,200</span></span>
   * <span data-ttu-id="27098-111">데이터 비트: 8</span><span class="sxs-lookup"><span data-stu-id="27098-111">Data bits: 8</span></span>
   * <span data-ttu-id="27098-112">정지 비트: 1</span><span class="sxs-lookup"><span data-stu-id="27098-112">Stop bits: 1</span></span>
   * <span data-ttu-id="27098-113">패리티: 없음</span><span class="sxs-lookup"><span data-stu-id="27098-113">Parity: None</span></span>
   * <span data-ttu-id="27098-114">흐름 제어: 없음</span><span class="sxs-lookup"><span data-stu-id="27098-114">Flow control: None</span></span>
     
     <span data-ttu-id="27098-115">이러한 설정은 hello 다음 그림에에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27098-115">These settings are shown in hello following illustration.</span></span>
     
     ![PuTTY 설정](./media/storsimple-use-putty/HCS_PuttyConfig-include.png) 
     
     > [!NOTE]
     > <span data-ttu-id="27098-117">Hello 기본 흐름 제어 설정이 작동 하지 않으면 hello 흐름 제어 tooXON/XOFF를 설정 해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="27098-117">If hello default flow control setting does not work, try setting hello flow control tooXON/XOFF.</span></span>
     > 
     > 
7. <span data-ttu-id="27098-118">클릭 **열려** toostart 직렬 세션입니다.</span><span class="sxs-lookup"><span data-stu-id="27098-118">Click **Open** toostart a serial session.</span></span>

