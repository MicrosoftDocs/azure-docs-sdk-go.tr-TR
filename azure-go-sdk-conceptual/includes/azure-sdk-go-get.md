[Go için Azure SDK](https://github.com/Azure/azure-sdk-for-go), Go 1.8 ve sonraki sürümlerle uyumludur. [Azure Stack Profilleri](https://docs.microsoft.com/en-us/azure/azure-stack/azure-stack-version-profiles) kullanan ortamlar için en az Go 1.9 sürümü gerekir.
Sisteminizde Go yoksa [Go yükleme yönergelerini](https://golang.org/doc/install) izleyin.

Go için Azure SDK ve bağımlılıklarını `go get` üzerinden edinebilirsiniz.

```bash
go get -u -d github.com/Azure/azure-sdk-for-go/...
```

> [!WARNING]
> URL’de `Azure` kısmını büyük harfle yazdığınızdan emin olun. Aksi takdirde bu, SDK ile çalışırken büyük/küçük harfle ilgili içeri aktarma sorunlarına neden olabilir. İçeri aktarma deyimlerinizde de `Azure` kısmını büyük harfle yazmanız gerekir.

