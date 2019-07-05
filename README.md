# POPIS

Open-source (CC&nbsp;BY-SA&nbsp;4) ASMR video, ve kterém předčítám výroky ze scénářů svého seriálu Ester Krejčí. Ve videu se vyskytují následující ASMR triggery: šeptání, listování, vlak. Současně také slouží jako booktrailer tohoto seriálu.

Snažil/a jsem se, aby byl tento projekt co nejotevřenější ve smyslu svobodného software, tedy zejména, aby umožňoval:

- Studovat, jak bylo dílo vytvořeno.
- Upravit dílo a upravenou verzi sestavit do finální podoby čistě pomocí svobodného software.

Vzhledem k tomu, že jsem ještě nevyzkoušel/a GitHub LFS, některé opravdu velké soubory s&nbsp;videem a&nbsp;zvuky jsem do repozitáře nahrál/a ve výrazně snížené kvalitě:

- videa/*.mp4
- zvuky/*.mp3 (ale „septani.mp3“ lze sestavit v&nbsp;plné kvalitě použitím níže uvedeného návodu)

Velikosti a kontrolní součtů původních souborů jsou uvedeny níže v sekci „ORIGINÁLNÍ SOUBORY“. Pokud budete mít zájem o&nbsp;sestavení projektu v&nbsp;plné kvalitě, napište mi o&nbsp;originální soubory na e-mail a pokusím se vám je zpřístupnit ke stažení:

singularis@volny.cz

# NÁVOD K SESTAVENÍ

Následující návody jsem otestoval/a na minimální instalaci Ubuntu 18.04.2 LTS.

## Potřebný software

- KDEnlive
- VLC Media Player
- Audacity (k sestavení šeptání)
- Kazam (k sestavení titulků)
- FFmpeg

Potřebné fonty:
- Latin Modern Sans (balíček „fonts-lmodern“, jen pro sestavení titulků)

## Sestavení videoprojektu

`$ sudo apt-get update`<br/>
`$ sudo apt-get install git kdenlive vlc`<br/>
`$ git clone https://github.com/singularis-mzf/booktrailer.git`<br/>
`$ cd booktrailer`<br/>
`$ kdenlive video.kdenlive`

- V KDEnlive kliknout na tlačítko Render.
- Nastavit rozumný výstupní soubor a případně i formát a kvalitu výstupu.

## Sestavení šeptání

`$ sudo apt install audacity`<br/>
`$ audacity septani.aup`

- File > Export > Export as MP3
- Nastavit při exportu dobrou kvalitu (ne nutně tu nejvyšší).
- Výsledkem přepsat zvuky/septani.mp3 (silně doporučuji nemít při tomto kroku otevřený projekt v&nbsp;KDEnlive).

## Sestavení závěrečných titulků
`$ sudo apt-get install firefox kazam fonts-lmodern vlc ffmpeg`

- Poznámka: místo balíčku „firefox“ můžete použít „firefox-esr“ (vyskytuje se v Debianu, případně lze získat z&nbsp;oficiálního PPA).

`$ kazam &`

- V programu Kazam nastavte: Screencast, Fullscreen, mouse cursor=FALSE, delay=5sec (nebo víc, pokud chcete).
- Před spuštěním musíte nastavit rozlišení obrazovky 1920x1080 nebo mírně větším (např. 1920x1200).

`$ firefox titulky/zaver.htm`

- Spustit záznam v Kazamu.
- Ve Firefoxu: F11 (na celou obrazovku) a F5 (obnovit stránku).
- Počkejte, než proběhnou všechny titulky (necelých 5 minut).
- Počkejte dalších 15 sekund jako rezervu.
- F11 (opustit režim celé obrazovky) a zavřete Firefox.
- V Kazamu vypněte záznam a výsledek uložte jako *videa/closing-base.mp4*.

`$ vlc videa/closing-base.mp4`

- Odhadněte v sekundách pozici ve videu, kdy se objeví první řádek titulků. Odečtěte 2 a výsledek použijte v&nbsp;následujícím příkazu místo „07“ (pokud vám vyšla 0, můžete parametr `-ss` i s jeho argumentem vynechat; je možné, že tento krok budete muset provést znovu s jinou hodnotou, aby výstup správně odpovídal zařazení v&nbsp;KDEnlive-projektu):

`$ ffmpeg -i videa/closing-base.mp4 -ss '00:00:07.000' -t 220 -c:v h264 -b:v 12743k -vf 'crop=1920:1080:-1:-1' -an -sn videa/closing.mp4`

## Očekávané problémy při sestavení

- Při prvním otevření projektu a po nahrazení jednotlivých vstupních souborů musí KDEnlive opravit soubor projektu. Pokud přitom neohlásí žádné nepřečtené či chybějící klipy, proběhl tento úkon vpořádku.
- Pokud při přehrávání neslyšíte zvuk, zkontrolujte hlasitost (jak v přehravači, tak systémovou, tak hardwarovou na reproduktorech).
- Rendering videa je náročný na paměť a výkon procesoru. Máte-li na počítači méně než 4 GiB RAM, pravděpodobně budete potřebovat velký swapovací soubor/oddíl a rendering potrvá velmi dlouho.

## Na co si dát pozor

Při úpravách šeptání si dejte pozor, aby se vám některá osa časově neposunula. Zařazení klipů do videa závisí na přesném načasování zvuku.

# ORIGINÁLNÍ SOUBORY

videa/closing.mp4:

- 310 914 990 bajtů
- MD5: df45e83a600e74c76656e38c37f4bc3f
- SHA256: feec7c07d12adbe6eaab72ac8b45b1026ea27c81c68381a62b6bfe6843aff3e9

videa/listovani.mp4:

- 1 077 900 245 bajtů
- MD5: b6b3d53723bf60ed4b98228520adb17a
- SHA256: da89c6b72e9df9b10d27b81d4a2731341ab4c96af33eaf8d1586d9660960a385

videa/prejezd.mp4:

- 96 310 928 bajtů
- MD5: d02be707fd1aaaefac07e9ce400fe3db
- SHA256: b375303a1ee2163c0258891cb8c868bc5b27e78361c75512693fbc707de2bf3f

videa/vlak.mp4:

- 60 891 374 bajtů
- MD5: 7c81e53694336a30c95b26120ca37069
- SHA256: 6ec680657fe4f612db1a87f1eaeff2540c80b731e8135f5158668297291539d2

zvuky/listovani.mp3:

- 21 116 236 bajtů
- MD5: 1f6cce4696c4f026e99cad05d1750500
- SHA256: 2e637417ae75782ea67f5e68a75c9cd4d9b0b2149cb6cdd7957565f943585c48

zvuky/septani.mp3:

- 17 164 696 bajtů
- MD5: 4149c6d20fa16f6a80162b3db62a54cd
- SHA256: 74f99991b95169467a28871611991ba49ece2fbfac6e4c9474918e70d1f8ce60

zvuky/tuxi.ogg:

- 1 835 803 bajtů
- MD5: da930d74c1f20a62856736a652fd1250
- SHA256: 4429918c23915c7893814b704cf242ed1fa382f2511eaf7949d46d9355490921


# COPYRIGHT

Celý projekt je možno používat, sdělovat veřejnosti a šířit pod podmínkami licence Creative Commons Attribution-ShareAlike 4.0 International, přiložené v&nbsp;souboru LICENSE. Podrobné údaje o&nbsp;autorství a&nbsp;licencích jednotlivých souborů jsou uvedeny v&nbsp;souboru COPYING.
