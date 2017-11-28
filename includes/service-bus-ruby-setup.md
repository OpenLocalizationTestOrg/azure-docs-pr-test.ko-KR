## <a name="create-a-ruby-application"></a><span data-ttu-id="b5051-101">Ruby 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="b5051-101">Create a Ruby application</span></span>
<span data-ttu-id="b5051-102">자세한 내용은 [Azure에서 Ruby 응용 프로그램 만들기](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b5051-102">For instructions, see [Create a Ruby Application on Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="b5051-103">서비스 버스를 사용하도록 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="b5051-103">Configure Your application to Use Service Bus</span></span>
<span data-ttu-id="b5051-104">Service Bus를 사용하려면 저장소 REST 서비스와 통신하는 편리한 라이브러리 집합이 포함된 Azure Ruby 패키지를 다운로드하여 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b5051-104">To use Service Bus, download and use the Azure Ruby package, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="b5051-105">RubyGems를 사용하여 패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="b5051-105">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="b5051-106">**PowerShell**(Windows), **Terminal**(Mac) 또는 **Bash**(Unix)와 같은 명령줄 인터페이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b5051-106">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="b5051-107">명령 창에 "gem install azure"를 입력하여 gem 및 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b5051-107">Type "gem install azure" in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="b5051-108">패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="b5051-108">Import the package</span></span>
<span data-ttu-id="b5051-109">원하는 텍스트 편집기를 사용하여 저장소를 사용하려는 Ruby 파일의 맨 위에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b5051-109">Using your favorite text editor, add the following to the top of the Ruby file in which you intend to use storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="b5051-110">서비스 버스 연결 설정</span><span class="sxs-lookup"><span data-stu-id="b5051-110">Set up a Service Bus connection</span></span>
<span data-ttu-id="b5051-111">다음 코드를 사용하여 네임스페이스, 키 이름, 키, 서명자 및 호스트에 대한 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b5051-111">Use the following code to set the values of namespace, name of the key, key, signer and host:</span></span>

```ruby
Azure.configure do |config|
  config.sb_namespace = '<your azure service bus namespace>'
  config.sb_sas_key_name = '<your azure service bus access keyname>'
  config.sb_sas_key = '<your azure service bus access key>'
end
signer = Azure::ServiceBus::Auth::SharedAccessSigner.new
sb_host = "https://#{Azure.sb_namespace}.servicebus.windows.net"
```

<span data-ttu-id="b5051-112">네임스페이스 값을 전체 URL이 아니라 만든 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b5051-112">Set the namespace value to the value you created rather than the entire URL.</span></span> <span data-ttu-id="b5051-113">예를 들어 "yourexamplenamespace.servicebus.windows.net"이 아니라 **"yourexamplenamespace"**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b5051-113">For example, use **"yourexamplenamespace"**, not "yourexamplenamespace.servicebus.windows.net".</span></span>
