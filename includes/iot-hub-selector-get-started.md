> [!div class="op_single_selector"]
> * [<span data-ttu-id="28430-101">C#</span><span class="sxs-lookup"><span data-stu-id="28430-101">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-getstarted.md)
> * [<span data-ttu-id="28430-102">Java</span><span class="sxs-lookup"><span data-stu-id="28430-102">Java</span></span>](../articles/iot-hub/iot-hub-java-java-getstarted.md)
> * [<span data-ttu-id="28430-103">Node.JS</span><span class="sxs-lookup"><span data-stu-id="28430-103">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-getstarted.md)
> * [<span data-ttu-id="28430-104">Python</span><span class="sxs-lookup"><span data-stu-id="28430-104">Python</span></span>](../articles/iot-hub/iot-hub-python-getstarted.md)
> 
> 

## <a name="introduction"></a><span data-ttu-id="28430-105">소개</span><span class="sxs-lookup"><span data-stu-id="28430-105">Introduction</span></span>
<span data-ttu-id="28430-106">Azure IoT Hub는 수백만의 IoT(사물 인터넷) 장치와 솔루션 백 엔드 간에서 안정적이고 안전한 양방향 통신이 가능하도록 완전히 관리되는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="28430-106">Azure IoT Hub is a fully managed service that enables reliable and secure bi-directional communications between millions of Internet of Things (IoT) devices and a solution back end.</span></span> <span data-ttu-id="28430-107">IoT 면 프로젝트는 hello 가장 큰 해결 과제 중 하나인 어떻게 tooreliably 장치 toohello 솔루션에 대 한 백 엔드를 안전 하 게 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="28430-107">One of hello biggest challenges that IoT projects face is how tooreliably and securely connect devices toohello solution back end.</span></span> <span data-ttu-id="28430-108">tooaddress이이 문제를 IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="28430-108">tooaddress this challenge, IoT Hub:</span></span>

* <span data-ttu-id="28430-109">신뢰할 수 있는 장치-클라우드 및 클라우드-장치 하이퍼 스케일 메시징을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="28430-109">Offers reliable device-to-cloud and cloud-to-device hyper-scale messaging.</span></span>
* <span data-ttu-id="28430-110">장치 단위 보안 자격 증명 및 액세스 제어를 사용하여 통신을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="28430-110">Enables secure communications using per-device security credentials and access control.</span></span>
* <span data-ttu-id="28430-111">Hello 가장 인기 있는 언어 및 플랫폼에 대 한 장치 라이브러리를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="28430-111">Includes device libraries for hello most popular languages and platforms.</span></span>

<span data-ttu-id="28430-112">이 자습서에서는 다음을 수행하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="28430-112">This tutorial shows you how to:</span></span>

* <span data-ttu-id="28430-113">Azure 포털 toocreate IoT hub hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="28430-113">Use hello Azure portal toocreate an IoT hub.</span></span>
* <span data-ttu-id="28430-114">IoT Hub에서 장치 ID를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28430-114">Create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="28430-115">원격 분석 tooyour 솔루션에 대 한 백 엔드 보내는 시뮬레이션 된 장치 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28430-115">Create a simulated device app that sends telemetry tooyour solution back end.</span></span>

