<span data-ttu-id="6f111-101">Azure 저장소의 모든 Blob은 컨테이너에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f111-101">Every blob in Azure storage must reside in a container.</span></span> <span data-ttu-id="6f111-102">hello 컨테이너의 일부를 구성 hello blob 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6f111-102">hello container forms part of hello blob name.</span></span> <span data-ttu-id="6f111-103">예를 들어 `mycontainer` hello 이러한 샘플 blob Uri에에서 hello 컨테이너 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6f111-103">For example, `mycontainer` is hello name of hello container in these sample blob URIs:</span></span>

    https://storagesample.blob.core.windows.net/mycontainer/blob1.txt
    https://storagesample.blob.core.windows.net/mycontainer/photos/myphoto.jpg

<span data-ttu-id="6f111-104">컨테이너 이름은 표준에 맞는 toohello 명명 규칙에 따라 유효한 DNS 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f111-104">A container name must be a valid DNS name, conforming toohello following naming rules:</span></span>

1. <span data-ttu-id="6f111-105">컨테이너 이름은 문자 또는 숫자로 시작 해야 하며 문자, 숫자 및 hello 대시 (-) 문자만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f111-105">Container names must start with a letter or number, and can contain only letters, numbers, and hello dash (-) character.</span></span>
2. <span data-ttu-id="6f111-106">컨테이너 이름에서 모든 대시(-) 문자는 문자 또는 숫자 바로 앞뒤에 와야 하며 연속 대시를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6f111-106">Every dash (-) character must be immediately preceded and followed by a letter or number; consecutive dashes are not permitted in container names.</span></span>
3. <span data-ttu-id="6f111-107">컨테이너 이름의 모든 문자는 소문자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f111-107">All letters in a container name must be lowercase.</span></span>
4. <span data-ttu-id="6f111-108">컨테이너 이름의 길이는 3자 이상, 63자 이하여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f111-108">Container names must be from 3 through 63 characters long.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6f111-109">해당 hello 확인 된 컨테이너의 이름을 항상 소문자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f111-109">Note that hello name of a container must always be lowercase.</span></span> <span data-ttu-id="6f111-110">컨테이너 이름에는 대문자를 포함 하거나 hello 컨테이너 명명 규칙을 위반 하는 그렇지 않은 경우 400 오류 (잘못 된 요청)를 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f111-110">If you include an upper-case letter in a container name, or otherwise violate hello container naming rules, you may receive a 400 error (Bad Request).</span></span> 
> 
> 

