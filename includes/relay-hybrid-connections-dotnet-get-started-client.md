### <a name="create-a-console-application"></a><span data-ttu-id="46613-101">콘솔 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="46613-101">Create a console application</span></span>

<span data-ttu-id="46613-102">먼저 Visual Studio를 시작하고 **콘솔 앱(.NET Framework)** 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="46613-102">First, launch Visual Studio and create a new **Console App (.NET Framework)** project.</span></span>

### <a name="add-hello-relay-nuget-package"></a><span data-ttu-id="46613-103">Hello 릴레이 NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="46613-103">Add hello Relay NuGet package</span></span>

1. <span data-ttu-id="46613-104">Hello 새로 만든 프로젝트를 마우스 오른쪽 단추로 누른 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="46613-104">Right-click hello newly created project and then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="46613-105">Hello 클릭 **찾아보기** 누른 "Microsoft.Azure.Relay" 및 선택 hello에 대 한 검색 **Microsoft Azure 릴레이** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="46613-105">Click hello **Browse** tab, then search for "Microsoft.Azure.Relay" and select hello **Microsoft Azure Relay** item.</span></span> <span data-ttu-id="46613-106">클릭 **설치** toocomplete hello 설치의 경우 다음이 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="46613-106">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>

### <a name="write-some-code-toosend-messages"></a><span data-ttu-id="46613-107">Toosend 메시지 일부 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="46613-107">Write some code toosend messages</span></span>

1. <span data-ttu-id="46613-108">Hello 기존 항목 바꾸기 `using` hello 다음과 같이 hello Program.cs 파일의 hello 위쪽 문을 `using` 문:</span><span class="sxs-lookup"><span data-stu-id="46613-108">Replace hello existing `using` statements at hello top of hello Program.cs file with hello following `using` statements:</span></span>
   
    ```csharp
    using System;
    using System.IO;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.Azure.Relay;
    ```
2. <span data-ttu-id="46613-109">상수 toohello 추가 `Program` hello 하이브리드 연결 세부 정보에 대 한 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="46613-109">Add constants toohello `Program` class for hello hybrid connection details.</span></span> <span data-ttu-id="46613-110">Hello 값 hello 하이브리드 연결을 만들 때 대괄호의 hello 자리 표시자를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="46613-110">Replace hello placeholders in brackets with hello values you obtained when creating hello hybrid connection.</span></span> <span data-ttu-id="46613-111">있는지 toouse hello 정규화 된 네임 스페이스 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46613-111">Be sure toouse hello fully qualified namespace name:</span></span>
   
    ```csharp
    private const string RelayNamespace = "{RelayNamespace}.servicebus.windows.net";
    private const string ConnectionName = "{HybridConnectionName}";
    private const string KeyName = "{SASKeyName}";
    private const string Key = "{SASKey}";
    ```
3. <span data-ttu-id="46613-112">다음 메서드 toohello hello 추가 `Program` 클래스:</span><span class="sxs-lookup"><span data-stu-id="46613-112">Add hello following method toohello `Program` class:</span></span>
   
    ```csharp
    private static async Task RunAsync()
    {
        Console.WriteLine("Enter lines of text toosend toohello server with ENTER");
   
        // Create a new hybrid connection client
        var tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(KeyName, Key);
        var client = new HybridConnectionClient(new Uri(String.Format("sb://{0}/{1}", RelayNamespace, ConnectionName)), tokenProvider);
   
        // Initiate hello connection
        var relayConnection = await client.CreateConnectionAsync();
   
        // We run two concurrent loops on hello connection. One 
        // reads input from hello console and writes it toohello connection 
        // with a stream writer. hello other reads lines of input from hello 
        // connection with a stream reader and writes them toohello console. 
        // Entering a blank line will shut down hello write task after 
        // sending it toohello server. hello server will then cleanly shut down
        // hello connection which will terminate hello read task.
   
        var reads = Task.Run(async () => {
            // Initialize hello stream reader over hello connection
            var reader = new StreamReader(relayConnection);
            var writer = Console.Out;
            do
            {
                // Read a full line of UTF-8 text up toonewline
                string line = await reader.ReadLineAsync();
                // if hello string is empty or null, we are done.
                if (String.IsNullOrEmpty(line))
                    break;
                // Write toohello console
                await writer.WriteLineAsync(line);
            }
            while (true);
        });
   
        // Read from hello console and write toohello hybrid connection
        var writes = Task.Run(async () => {
            var reader = Console.In;
            var writer = new StreamWriter(relayConnection) { AutoFlush = true };
            do
            {
                // Read a line form hello console
                string line = await reader.ReadLineAsync();
                // Write hello line out, also when it's empty
                await writer.WriteLineAsync(line);
                // Quit when hello line was empty
                if (String.IsNullOrEmpty(line))
                    break;
            }
            while (true);
        });
   
        // Wait for both tasks toocomplete
        await Task.WhenAll(reads, writes);
        await relayConnection.CloseAsync(CancellationToken.None);
    }
    ```
4. <span data-ttu-id="46613-113">다음 줄의 코드 toohello hello 추가 `Main` hello에 대 한 메서드 `Program` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="46613-113">Add hello following line of code toohello `Main` method in hello `Program` class.</span></span>
   
    ```csharp
    RunAsync().GetAwaiter().GetResult();
    ```
   
    <span data-ttu-id="46613-114">Program.cs는 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46613-114">Here is what your Program.cs should look like.</span></span>
   
    ```csharp
    using System;
    using System.IO;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.Azure.Relay;
   
    namespace Client
    {
        class Program
        {
            private const string RelayNamespace = "{RelayNamespace}.servicebus.windows.net";
            private const string ConnectionName = "{HybridConnectionName}";
            private const string KeyName = "{SASKeyName}";
            private const string Key = "{SASKey}";
   
            static void Main(string[] args)
            {
                RunAsync().GetAwaiter().GetResult();
            }
   
            private static async Task RunAsync()
            {
                Console.WriteLine("Enter lines of text toosend toohello server with ENTER");
   
                // Create a new hybrid connection client
                var tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(KeyName, Key);
                var client = new HybridConnectionClient(new Uri(String.Format("sb://{0}/{1}", RelayNamespace, ConnectionName)), tokenProvider);
   
                // Initiate hello connection
                var relayConnection = await client.CreateConnectionAsync();
   
                // We run two conucrrent loops on hello connection. One 
                // reads input from hello console and writes it toohello connection 
                // with a stream writer. hello other reads lines of input from hello 
                // connection with a stream reader and writes them toohello console. 
                // Entering a blank line will shut down hello write task after 
                // sending it toohello server. hello server will then cleanly shut down
                // hello connection which will terminate hello read task.
   
                var reads = Task.Run(async () => {
                    // Initialize hello stream reader over hello connection
                    var reader = new StreamReader(relayConnection);
                    var writer = Console.Out;
                    do
                    {
                        // Read a full line of UTF-8 text up toonewline
                        string line = await reader.ReadLineAsync();
                        // If hello string is empty or null, we are done.
                        if (String.IsNullOrEmpty(line))
                            break;
                        // Write toohello console
                        await writer.WriteLineAsync(line);
                    }
                    while (true);
                });
   
                // Read from hello console and write toohello hybrid connection
                var writes = Task.Run(async () => {
                    var reader = Console.In;
                    var writer = new StreamWriter(relayConnection) { AutoFlush = true };
                    do
                    {
                        // Read a line form hello console
                        string line = await reader.ReadLineAsync();
                        // Write hello line out, also when it's empty
                        await writer.WriteLineAsync(line);
                        // Quit when hello line was empty
                        if (String.IsNullOrEmpty(line))
                            break;
                    }
                    while (true);
                });
   
                // Wait for both tasks toocomplete
                await Task.WhenAll(reads, writes);
                await relayConnection.CloseAsync(CancellationToken.None);
            }
        }
    }
    ```

