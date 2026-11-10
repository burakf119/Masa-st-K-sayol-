# Masaüstü Kısa Yol Kaldırma
# Ok Kaldır

Windows masaüstündeki kısayol ikonlarının köşesinde çıkan küçük okları tek tıkla kaldıran (ve istenince geri getiren) küçük bir program.

*English version below.*

## İndirme

Sağdaki **Releases** bölümünden `OkKaldir.zip` dosyasını indirin, zipten çıkarın ve `OkKaldir.exe` dosyasını çalıştırın. Kurulum gerekmez.

## Kullanım

1. `OkKaldir.exe` dosyasına çift tıklayın, yönetici izni sorulursa **Evet** deyin.
2. Açılan pencerede seçin:
   - **Evet:** kısayol oklarını kaldırır
   - **Hayır:** okları geri getirir
   - **İptal:** hiçbir şey yapmadan çıkar
3. Masaüstü birkaç saniyeliğine kapanıp açılır, bu normaldir.

Oklar gitmediyse bilgisayarı yeniden başlatın. Bazı Windows 11 sürümlerinde ayar ancak yeniden başlatınca görünür.

## Sık sorulanlar

**Windows "bilinmeyen yayıncı" uyarısı veriyor.**
Program dijital olarak imzalı değil. "Ek bilgi" → "Yine de çalıştır" ile açabilirsiniz. Güvenmiyorsanız kaynak kodu bu depoda, kendiniz inceleyip derleyebilirsiniz.

**Antivirüsüm uyarı verdi.**
Program yönetici izni ister, kayıt defterine tek bir değer yazar ve Windows Gezgini'ni yeniden başlatır. Bazı antivirüsler bu davranışı şüpheli sayabilir. Ne yaptığı aşağıda açıkça yazıyor.

**Sadece bazı ikonların okunu kaldırabilir miyim?**
Hayır. Windows bu ayarı ikon bazında desteklemiyor; oklar ya hepsinde vardır ya hiçbirinde.

## Program tam olarak ne yapıyor?

- `C:\ProgramData\OkKaldir\blank.ico` adında boş (şeffaf) bir ikon dosyası oluşturur.
- Kayıt defterinde `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Shell Icons` altındaki `29` değerini bu ikona yönlendirir.
- İkon önbelleğini temizler ve Windows Gezgini'ni yeniden başlatır.

Geri alma işlemi `29` değerini siler ve Gezgini yeniden başlatır. Program internete bağlanmaz, başka hiçbir dosyaya veya ayara dokunmaz.

## Kaynaktan derleme

[Go](https://go.dev/dl/) kurulu olmalı:

```
go build -trimpath -ldflags "-H windowsgui -s -w" -o OkKaldir.exe .
```

Program simgesi `rsrc_windows_amd64.syso` dosyasından gelir; derleme sırasında otomatik eklenir.

## Sorumluluk reddi

Bu program olduğu gibi, hiçbir garanti verilmeden sunulur. Kullanım sorumluluğu kullanıcıya aittir. Microsoft ile hiçbir bağlantısı yoktur. Ayrıntılar için [LICENSE](LICENSE) dosyasına bakın.

---

# Ok Kaldır (Shortcut Arrow Remover)

A tiny Windows tool that removes the small arrow overlay from shortcut icons with one click, and can bring it back the same way.

## Download

Get `OkKaldir.zip` from the **Releases** section, extract it and run `OkKaldir.exe`. No installation needed.

## Usage

1. Double-click `OkKaldir.exe` and accept the administrator prompt.
2. Choose in the dialog (the dialog text is in Turkish):
   - **Yes (Evet):** remove the shortcut arrows
   - **No (Hayır):** restore the arrows
   - **Cancel (İptal):** exit without changes
3. The desktop disappears for a few seconds while Explorer restarts. This is expected.

If the arrows are still there, reboot. On some Windows 11 builds the change only shows up after a restart.

## FAQ

**Windows shows an "unknown publisher" warning.**
The executable is not code-signed. Click "More info" → "Run anyway". If you prefer, read the source in this repository and build it yourself.

**My antivirus flagged it.**
The tool asks for administrator rights, writes one registry value and restarts Explorer. Some antivirus products treat that as suspicious. Everything it does is listed below.

**Can I remove the arrow from only some icons?**
No. Windows does not support this per icon; the overlay is either on for all shortcuts or off for all.

## What exactly does it do?

- Creates an empty (transparent) icon at `C:\ProgramData\OkKaldir\blank.ico`.
- Points the `29` value under `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Shell Icons` to that icon.
- Clears the icon cache and restarts Windows Explorer.

Restoring deletes the `29` value and restarts Explorer. The tool never connects to the internet and touches no other files or settings.

## Building from source

Requires [Go](https://go.dev/dl/):

```
go build -trimpath -ldflags "-H windowsgui -s -w" -o OkKaldir.exe .
```

The application icon comes from `rsrc_windows_amd64.syso`, which the Go toolchain links in automatically.

## Disclaimer

This software is provided as is, without warranty of any kind. Use it at your own risk. It is not affiliated with Microsoft. See [LICENSE](LICENSE) for details.
