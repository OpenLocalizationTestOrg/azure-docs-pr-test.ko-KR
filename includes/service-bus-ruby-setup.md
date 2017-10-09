## <a name="create-a-ruby-application"></a><span data-ttu-id="84370-101">Ruby 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="84370-101">Create a Ruby application</span></span>
<span data-ttu-id="84370-102">자세한 내용은 [Azure에서 Ruby 응용 프로그램 만들기](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="84370-102">For instructions, see [Create a Ruby Application on Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="84370-103">사용자 응용 프로그램 tooUse 서비스 버스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="84370-103">Configure Your application tooUse Service Bus</span></span>
<span data-ttu-id="84370-104">서비스 버스 toouse 다운로드 하 여 hello 저장소 REST 서비스와 통신 하는 편리한 라이브러리의 집합을 포함 하는 hello Azure Ruby 패키지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="84370-104">toouse Service Bus, download and use hello Azure Ruby package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="84370-105">RubyGems tooobtain hello 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="84370-105">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="84370-106">**PowerShell**(Windows), **Terminal**(Mac) 또는 **Bash**(Unix)와 같은 명령줄 인터페이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="84370-106">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="84370-107">"보석" 설치 azure의 hello 명령 창 tooinstall hello 보석 및 종속성을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="84370-107">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="84370-108">Hello 패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="84370-108">Import hello package</span></span>
<span data-ttu-id="84370-109">원하는 텍스트 편집기를 사용 하 여 추가 hello hello Ruby toohello 맨 뒤 toouse 저장 하려는 파일:</span><span class="sxs-lookup"><span data-stu-id="84370-109">Using your favorite text editor, add hello following toohello top of hello Ruby file in which you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="84370-110">서비스 버스 연결 설정</span><span class="sxs-lookup"><span data-stu-id="84370-110">Set up a Service Bus connection</span></span>
<span data-ttu-id="84370-111">사용 하 여 hello 다음 코드의 네임 스페이스, 이름 hello의 tooset hello 값 키, 키, 서명자 및 호스트:</span><span class="sxs-lookup"><span data-stu-id="84370-111">Use hello following code tooset hello values of namespace, name of hello key, key, signer and host:</span></span>

```ruby
Azure.configure do |config|
  config.sb_namespace = '<your azure service bus namespace>'
  config.sb_sas_key_name = '<your azure service bus access keyname>'
  config.sb_sas_key = '<your azure service bus access key>'
end
signer = Azure::ServiceBus::Auth::SharedAccessSigner.new
sb_host = "https://#{Azure.sb_namespace}.servicebus.windows.net"
```

<span data-ttu-id="84370-112">Hello 전체 URL 대신 생성 하는 hello 네임 스페이스 값 toohello 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="84370-112">Set hello namespace value toohello value you created rather than hello entire URL.</span></span> <span data-ttu-id="84370-113">예를 들어 "yourexamplenamespace.servicebus.windows.net"이 아니라 **"yourexamplenamespace"**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="84370-113">For example, use **"yourexamplenamespace"**, not "yourexamplenamespace.servicebus.windows.net".</span></span>
