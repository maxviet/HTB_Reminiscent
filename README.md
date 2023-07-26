### HTB_Reminiscent
<br>

##### Aufgabe:
[Die Challenge Website](https://app.hackthebox.com/challenges/Reminiscent)

Verdächtiger Datenverkehr wurde von einem Recruiter-PC festgestellt. Ein Speicherauszug wurde vor der Netzwerktrennung erfasst. Der Recruiter erhielt eine E-Mail bezüglich eines Lebenslaufs. Diese E-Mail wurde wiederhergestellt. Ziel ist es, die Malware-Quelle zu finden und zu entschlüsseln, um die Flagge zu ermitteln.

<br>

##### Die verwendeten Tools und Techniken.
In dieser Capture The Flag (CTF) Herausforderung liegt der Fokus auf der Nutzung des Tools **Volatility**, der Arbeit mit der Bash-Konsole und allgemeinen Konsolenoperationen. Volatility ist ein wesentliches Werkzeug in der digitalen Forensik und ermöglicht es uns, forensische Artefakte aus dem Speicher (RAM) zu extrahieren und zu analysieren. Es ist besonders nützlich bei der Untersuchung von Systemkompromittierungen, bei denen der volatile Speicher oft wertvolle Hinweise auf den Angriffsprozess liefert. Eine detaillierte Beschreibung von Volatility, seiner Hauptanwendungen und wie es speziell für diese Herausforderung genutzt wird, finden Sie in den anderen .md-Dateien dieses Repositories.

Die **Bash-Konsole** ist ein mächtiges Werkzeug, das uns erlaubt, eine Vielzahl von Aufgaben effizient auszuführen. In dieser Herausforderung nutzen wir sie für verschiedene Aufgaben, einschließlich der Arbeit mit Dateien und der Ausführung von Befehlen.

Ursprünglich war geplant, *Cyberchef* für die Verschlüsselungsaufgaben zu verwenden. Cyberchef ist ein webbasiertes Tool, das eine Vielzahl von Verschlüsselungs- und Kodierungsmethoden unterstützt. Leider gab es einige technische Probleme mit der Website, die die Nutzung erschwerten. Daher wurde entschieden, stattdessen das Bash-Terminal für diese Aufgaben zu verwenden. Obwohl dies eine Herausforderung darstellte, bot es auch eine wertvolle Gelegenheit, die Fähigkeiten im Umgang mit der Bash-Konsole zu vertiefen und zu erweitern.

Insgesamt bot diese CTF eine umfassende und praktische Einführung in einige der wichtigsten Tools und Techniken, die in der digitalen Forensik eingesetzt werden. Es war eine wertvolle Erfahrung, die dazu beitrug, die Fähigkeiten und das Verständnis in diesem wichtigen Bereich zu erweitern.

<br>

##### Eine Zusammenfassung der Lösung

Zuerst analysieren wir den Speicherauszug "flounder-pc-memdump.elf" mit Volatility. Das ist ein Tool, das uns hilft, Informationen aus dem Arbeitsspeicher eines Computers zu holen.

Bevor wir loslegen, müssen wir herausfinden, welches Profil wir in Volatility verwenden sollen. Das ist wichtig, weil jedes Betriebssystem Informationen etwas anders im Speicher ablegt. In diesem Fall verwenden wir das Profil "Win7SP1x64_23418".

Als nächstes schauen wir uns an, welche Prozesse auf dem Computer liefen, als der Speicherauszug gemacht wurde. Dafür verwenden wir das Plugin "pstree" in Volatility. Damit können wir sehen, welche Prozesse liefen und welche anderen Prozesse sie gestartet haben.

In der Liste der Prozesse sehen wir etwas Verdächtiges: Das E-Mail-Programm Thunderbird hat einen Prozess namens "powershell" gestartet. Das ist ungewöhnlich und könnte ein Hinweis darauf sein, dass etwas nicht stimmt.

Wir erinnern uns, dass der Recruiter gesagt hat, dass er eine E-Mail mit einem Lebenslauf erhalten hat. Vielleicht hat er diese E-Mail mit Thunderbird geöffnet und dabei versehentlich einen schädlichen Anhang geöffnet.

Um das zu überprüfen, suchen wir auf dem Computer nach einer Datei namens "resume". Und tatsächlich, wir finden eine Datei namens "resume.pdf.lnk". LNK-Dateien sind normalerweise Verknüpfungen, die man auf dem Desktop oder im Startmenü findet.

Jetzt wollen wir uns diese LNK-Datei genauer ansehen. Dafür "dumpen" wir sie, das heißt, wir holen sie aus dem Speicherauszug und speichern sie als eigene Datei.

Wenn wir uns die gedumpte LNK-Datei ansehen, finden wir darin einen Base64-kodierten String. Das ist eine Art, Daten zu kodieren, so dass sie als Text dargestellt werden können.

Mit dem Online-Tool Cyberchef können wir diesen Base64-String dekodieren und sehen, dass es sich um einen weiteren Powershell-Befehl handelt. Das ist ein weiterer Hinweis darauf, dass hier etwas nicht stimmt.

<br>

##### Eventuell ein Verweis auf detailliertere Dokumentationen in anderen Dateien.

