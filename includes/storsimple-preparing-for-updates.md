<!--author=jgerend last changed: 03/16/16-->

## <a name="preparing-for-updates"></a><span data-ttu-id="bf214-101">업데이트 준비</span><span class="sxs-lookup"><span data-stu-id="bf214-101">Preparing for updates</span></span>
<span data-ttu-id="bf214-102">다음 단계를 검색 하 고 hello 업데이트를 적용 하기 전에 tooperform hello이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf214-102">You will need tooperform hello following steps before you scan and apply hello update:</span></span>

1. <span data-ttu-id="bf214-103">Hello 장치 데이터의 클라우드 스냅숏을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf214-103">Take a cloud snapshot of hello device data.</span></span>
2. <span data-ttu-id="bf214-104">컨트롤러 고정 Ip 라우팅할 수 있고 toohello 인터넷에 연결할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf214-104">Ensure that your controller fixed IPs are routable and can connect toohello Internet.</span></span> <span data-ttu-id="bf214-105">이러한 고정 Ip를 사용 하는 tooservice 업데이트 tooyour 장치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf214-105">These fixed IPs will be used tooservice updates tooyour device.</span></span> <span data-ttu-id="bf214-106">Hello 장치의 hello Windows PowerShell 인터페이스에서 각 컨트롤러에서 cmdlet 뒤 hello를 실행 하 여이 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf214-106">You can test this by running hello following cmdlet on each controller from hello Windows PowerShell interface of hello device:</span></span>
   
     `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter network> `
   
    <span data-ttu-id="bf214-107">**고정된 Ip toohello 인터넷에 연결할 수 있는 경우 테스트 연결에 대 한 샘플 출력**</span><span class="sxs-lookup"><span data-stu-id="bf214-107">**Sample output for Test-Connection when fixed IPs can connect toohello Internet**</span></span>

        Controller0>Test-Connection -Source 10.126.173.91 -Destination bing.com

        Source      Destination     IPV4Address      IPV6Address
        ----------------- -----------  -----------
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200

        Controller0>Test-Connection -Source 10.126.173.91 -Destination  204.79.197.200

        Source      Destination       IPV4Address    IPV6Address
        ----------------- -----------  -----------
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200

<span data-ttu-id="bf214-108">이러한 수동 사전 검사 성공적으로 마치면 tooscan 진행 하 고 hello 업데이트를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf214-108">After you have successfully completed these manual pre-checks, you can proceed tooscan and install hello updates.</span></span>

