# POPIS

Open-source (CC&nbsp;BY-SA&nbsp;4) ASMR video, ve kterém předčítám výroky ze scénářů svého seriálu Ester Krejčí. Ve videu se vyskytují následující ASMR triggery: šeptání, listování, vlak. Současně také slouží jako booktrailer tohoto seriálu.

Snažil/a jsem se, aby byl tento projekt co nejotevřenější ve smyslu svobodného software, tedy zejména, aby umožňoval:

- Studovat, jak bylo dílo vytvořeno.
- Upravit dílo a upravenou verzi sestavit do finální podoby čistě pomocí svobodného software.

Vzhledem k tomu, že jsem ještě nevyzkoušel/a GitHub LFS, některé opravdu velké soubory s&nbsp;videem a&nbsp;zvuky jsem do repozitáře nahrál/a ve výrazně snížené kvalitě:

- videa/*.mp4
- zvuky/*.mp3 (ale „septani.mp3“ lze sestavit v&nbsp;plné kvalitě použitím níže uvedeného návodu)

Pro vývoj to celkem stačí. Pokud budete mít zájem o&nbsp;sestavení projektu v&nbsp;plné kvalitě, napište mi o&nbsp;dané soubory na e-mail a pokusím se vám je zpřístupnit ke stažení:

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

# COPYRIGHT

Celý projekt je možno používat, sdělovat veřejnosti a šířit pod podmínkami licence Creative Commons Attribution-ShareAlike 4.0 International, přiložené v&nbsp;souboru LICENSE. Podrobné údaje o&nbsp;autorství a&nbsp;licencích jednotlivých souborů jsou uvedeny v&nbsp;souboru COPYING.
