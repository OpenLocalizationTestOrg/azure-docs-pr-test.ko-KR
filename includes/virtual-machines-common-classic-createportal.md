

<span data-ttu-id="81acf-101">*사용자 지정* 가상 컴퓨터란 간단하게 말해서 **Marketplace**의 **기능을 갖춘 앱**을 사용하여 만드는 가상 컴퓨터를 의미합니다. 이러한 가상 컴퓨터를 만드는 이유는 사용자를 대신하여 대부분의 작업을 수행하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="81acf-101">A *custom* virtual machine simply means a virtual machine that you create using a **Featured app** from the **Marketplace** because it does much of the work for you.</span></span> <span data-ttu-id="81acf-102">하지만 여전히 다음과 같은 항목이 포함된 구성을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81acf-102">Yet, you can still make configuration choices that include the following items:</span></span>

* <span data-ttu-id="81acf-103">가상 네트워크에 가상 컴퓨터 연결</span><span class="sxs-lookup"><span data-stu-id="81acf-103">Connecting the virtual machine to a virtual network.</span></span>
* <span data-ttu-id="81acf-104">맬웨어 방지 등, Azure Virtual Machine Agent 및 Azure Virtual Machine Extensions 설치</span><span class="sxs-lookup"><span data-stu-id="81acf-104">Installing the Azure Virtual Machine Agent and Azure Virtual Machine Extensions, such as for antimalware.</span></span>
* <span data-ttu-id="81acf-105">기존 클라우드 서비스에 가상 컴퓨터 추가</span><span class="sxs-lookup"><span data-stu-id="81acf-105">Adding the virtual machine to existing cloud services.</span></span>
* <span data-ttu-id="81acf-106">기존 저장소 계정에 가상 컴퓨터 추가</span><span class="sxs-lookup"><span data-stu-id="81acf-106">Adding the virtual machine to an existing Storage account.</span></span>
* <span data-ttu-id="81acf-107">가상 컴퓨터를 가용성 집합에 추가</span><span class="sxs-lookup"><span data-stu-id="81acf-107">Adding the virtual machine to an availability set.</span></span>

<!--
> [!IMPORTANT]
> If you want your virtual machine to use a virtual network so you can connect to it directly by host name or set up cross-premises connections, make sure that you specify the virtual network when you create the virtual machine. A virtual machine can be configured to join a virtual network only when you create the virtual machine. For details on virtual networks, see [Azure Virtual Network overview](../articles/virtual-network/virtual-networks-overview.md).
>
>
 -->

> [!IMPORTANT]
> <span data-ttu-id="81acf-108">가상 네트워크를 사용하는 가상 컴퓨터를 만들려면 가상 컴퓨터를 만들 때 가상 네트워크를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81acf-108">If you want your virtual machine to use a virtual network, make sure that you specify the virtual network when you create the virtual machine.</span></span>

> * <span data-ttu-id="81acf-109">가상 네트워크를 사용할 때 얻을 수 있는 두 가지 이점은 가상 컴퓨터에 직접 연결한다는 점과 프레미스 간 연결을 설정한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="81acf-109">Two benefits of using a virtual network are connecting directly to the virtual machine and to set up cross-premises connections.</span></span>

> * <span data-ttu-id="81acf-110">가상 컴퓨터를 만드는 경우에만 가상 네트워크에 가입하도록 가상 컴퓨터를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81acf-110">A virtual machine can be configured to join a virtual network only when you create the virtual machine.</span></span> <span data-ttu-id="81acf-111">가상 네트워크에 대한 자세한 내용은 [Azure 가상 네트워크 개요](../articles/virtual-network/virtual-networks-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81acf-111">For details on virtual networks, see [Azure Virtual Network overview](../articles/virtual-network/virtual-networks-overview.md).</span></span>
>
>

## <a name="to-create-the-virtual-machine"></a><span data-ttu-id="81acf-112">가상 컴퓨터를 만들려면</span><span class="sxs-lookup"><span data-stu-id="81acf-112">To create the virtual machine</span></span>
