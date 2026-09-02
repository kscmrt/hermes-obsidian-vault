# CAD Dosya Dönüştürme (DWG -> PDF)

Sunucuda DWG/DXF dosyalarını PDF'e dönüştürmek için QCAD CLI aracı yapılandırılmıştır.

## Konum
- Araç dizini: `/home/kscmrt/.local/qcad/`
- Binary / Symlink: `/home/kscmrt/.local/bin/dwg2pdf`

## Kullanım Komutu (Headless / Sunucu)
```bash
/home/kscmrt/.local/qcad/dwg2pdf -platform offscreen -a -auto-orientation -c -f -o "/cikis/yolu/dosya.pdf" "/giris/yolu/dosya.dwg"
```

## Parametreler
- `-platform offscreen`: X11/ekran sunucusu olmadan çalışmayı sağlar (Linux headless sunucular için zorunlu).
- `-a` (`-auto-fit`): Çizimi sayfaya sığdırır.
- `-auto-orientation`: Sayfa yönlendirmesini (yatay/dikey) çizim sınırlarına göre otomatik ayarlar.
- `-c`: Çizimi sayfada ortalar.
- `-f`: Var olan çıktı dosyasının üzerine yazar.
