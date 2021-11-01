# Best Practices für TensorFlow-Tests

Dies sind die empfohlenen Vorgehensweisen zum Testen von Code im [TensorFlow-Repository](https://github.com/tensorflow/tensorflow) .

## Bevor Sie beginnen

Bevor Sie Quellcode zu einem TensorFlow-Projekt beitragen, überprüfen Sie bitte die `CONTRIBUTING.md` im GitHub-Repository des Projekts. (Siehe beispielsweise die [Datei CONTRIBUTING.md für das Kernrepo von TensorFlow](https://github.com/tensorflow/tensorflow/blob/master/CONTRIBUTING.md) .) Alle Code-Mitwirkenden müssen eine [Contributor License Agreement](https://cla.developers.google.com/clas) (CLA) unterzeichnen.

## Status

passed retest

## Allgemeine Grundsätze

### Hängt nur davon ab, was du in deinen BUILD-Regeln verwendest

TensorFlow ist eine große Bibliothek und abhängig vom vollständigen Paket beim Schreiben eines Komponententests für seine Untermodule war eine gängige Praxis. Dadurch wird jedoch die `bazel` abhängigkeitsbasierte Analyse deaktiviert. Dies bedeutet, dass Continuous-Integration-Systeme nicht verwandte Tests für Pre-Submit-/Post-Submit-Läufe nicht intelligent eliminieren können. Wenn Sie sich nur auf die Submodule verlassen, die Sie in Ihrer `BUILD` Datei testen, sparen Sie Zeit für alle TensorFlow-Entwickler und viel wertvolle Rechenleistung.

Das Ändern Ihrer Build-Abhängigkeit zum Weglassen der vollständigen TF-Ziele bringt jedoch einige Einschränkungen für das, was Sie in Ihren Python-Code importieren können, mit sich. Sie können den `import tensorflow as tf` Anweisung in Ihren Unit-Tests verwenden. Dies ist jedoch ein lohnender Kompromiss, da es alle Entwickler vor Tausenden unnötiger Tests erspart.

### Jeder Code sollte Unit-Tests haben

Für jeden Code, den Sie schreiben, sollten Sie auch die Komponententests schreiben. Wenn Sie eine neue Datei `foo.py` schreiben, sollten Sie deren Unit-Tests in `foo_test.py` und innerhalb derselben Änderung einreichen. Streben Sie eine inkrementelle Testabdeckung von &gt;90 % für Ihren gesamten Code an.

## QIWI

FUUU
BEEE

### Vermeiden Sie die Verwendung von nativen Bazel-Testregeln in TF

TF hat viele Feinheiten beim Ausführen von Tests. Wir haben daran gearbeitet, all diese Komplexitäten in unseren Bazel-Makros zu verbergen. Um sich nicht mit diesen befassen zu müssen, verwenden Sie die folgenden anstelle der nativen Testregeln. Beachten Sie, dass all dies in `tensorflow/tensorflow.bzl` definiert ist. Verwenden Sie für CC-Tests `tf_cc_test` , `tf_gpu_cc_test` , `tf_gpu_only_cc_test` . `tf_py_test` für Python-Tests tf_py_test oder `gpu_py_test` . Wenn Sie etwas benötigen, das der nativen `py_test` Regel sehr nahe kommt, verwenden Sie stattdessen die in tensorflow.bzl definierte. Sie müssen nur die folgende Zeile am Anfang der BUILD-Datei hinzufügen: `load(“tensorflow/tensorflow.bzl”, “py_test”)`

### Seien Sie sich bewusst, wo der Test ausgeführt wird

Wenn Sie einen Test schreiben, kann sich unsere Testinfra darum kümmern, Ihre Tests auf CPU, GPU und Beschleunigern auszuführen, wenn Sie sie entsprechend schreiben. Wir haben automatisierte Tests, die auf Linux, Macos, Windows laufen, die Systeme mit oder ohne GPUs haben. Sie müssen lediglich eines der oben aufgeführten Makros auswählen und dann Tags verwenden, um den Ort ihrer Ausführung einzuschränken.

- `manual` Tag wird Ihren Test von der Ausführung überall ausschließen. Dazu gehören manuelle Testausführungen, die Muster wie `bazel test tensorflow/…`

- `no_oss` schließt Ihren Test von der Ausführung in der offiziellen TF OSS-Testinfrastruktur aus.

- `no_mac` Tags no_mac oder `no_windows` können verwendet werden, um Ihren Test von relevanten Betriebssystem-Testsuiten auszuschließen.

- `no_gpu` Tag kann verwendet werden, um Ihren Test von der Ausführung in GPU-Testsuiten auszuschließen.

### Überprüfen Sie die Tests, die in den erwarteten Testsuiten ausgeführt werden

TF hat einige Testsuiten. Manchmal kann die Einrichtung verwirrend sein. Es kann verschiedene Probleme geben, die dazu führen, dass Ihre Tests bei fortlaufenden Builds ausgelassen werden. Daher sollten Sie überprüfen, ob Ihre Tests wie erwartet ausgeführt werden. Um dies zu tun:

- Warten Sie, bis Ihre Pre-Submits auf Ihrem Pull Request (PR) vollständig ausgeführt wurden.
- Scrollen Sie zum Ende Ihres PR, um die Statusprüfungen anzuzeigen.
- Klicken Sie auf den Link „Details“ auf der rechten Seite eines Kokoro-Checks.
- Überprüfen Sie die Liste "Ziele", um Ihre neu hinzugefügten Ziele zu finden.

### Jede Klasse/Einheit sollte ihre eigene Komponententestdatei haben

Separate Testklassen helfen uns, Fehler und Ressourcen besser zu isolieren. Sie führen zu viel kürzeren und einfacher zu lesenden Testdateien. Daher sollten alle Ihre Python-Dateien mindestens eine entsprechende Testdatei haben (für jede `foo.py` sollte sie `foo_test.py` ). Für aufwändigere Tests wie Integrationstests, die unterschiedliche Setups erfordern, ist es in Ordnung, weitere Testdateien hinzuzufügen.

## Geschwindigkeit und Laufzeiten

### Sharding sollte so wenig wie möglich verwendet werden

Anstatt zu splittern, bedenken Sie bitte:

- Machen Sie Ihre Tests kleiner
- Wenn das oben genannte nicht möglich ist, teilen Sie die Tests auf

Sharding hilft, die Gesamtlatenz eines Tests zu reduzieren, aber das gleiche kann erreicht werden, indem Tests auf kleinere Ziele aufgeteilt werden. Das Aufteilen von Tests gibt uns eine feinere Kontrolle bei jedem Test, minimiert unnötige Pre-Submit-Läufe und reduziert den Abdeckungsverlust, wenn ein Buildcop ein gesamtes Ziel aufgrund eines fehlerhaften Testfalls deaktiviert. Darüber hinaus entstehen beim Sharding versteckte Kosten, die nicht so offensichtlich sind, z. B. das Ausführen des gesamten Testinitialisierungscodes für alle Shards. Dieses Problem wurde uns von Infra-Teams als eine Quelle eskaliert, die zusätzliche Belastung verursacht.

### Kleinere Tests sind besser

Je schneller Ihre Tests ausgeführt werden, desto wahrscheinlicher ist es, dass Personen Ihre Tests ausführen. Eine zusätzliche Sekunde für Ihren Test kann sich zu Stunden zusätzlicher Zeit ansammeln, die Entwickler und unsere Infrastruktur mit der Durchführung Ihres Tests verbringen. Versuchen Sie, Ihre Tests unter 30 Sekunden auszuführen (im Nicht-Opt-Modus!), und machen Sie sie klein. Markieren Sie Ihre Tests nur als letzten Ausweg als mittel. Die infra führt keine großen Tests als Presubmits oder Postsubmits durch! Schreiben Sie daher nur dann einen großen Test, wenn Sie festlegen möchten, wo er ausgeführt werden soll. Einige Tipps, damit Tests schneller ausgeführt werden:

- Führen Sie in Ihrem Test weniger Trainingseinheiten durch
- Erwägen Sie die Verwendung von Dependency Injection, um starke Abhängigkeiten des getesteten Systems durch einfache Fälschungen zu ersetzen.
- Erwägen Sie die Verwendung kleinerer Eingabedaten in Komponententests
- Wenn nichts anderes funktioniert, versuchen Sie, Ihre Testdatei aufzuteilen.

### Die Testzeiten sollten die Hälfte der Testgröße-Zeitüberschreitung anstreben, um Flocken zu vermeiden

Bei `bazel` Testzielen haben kleine Tests Zeitüberschreitungen von 1 Minute. Mittlere Test-Timeouts sind 5 Minuten. Große Tests werden vom TensorFlow-Test infra einfach nicht ausgeführt. Viele Tests sind jedoch nicht deterministisch in der Zeit, die sie benötigen. Aus verschiedenen Gründen können Ihre Tests hin und wieder mehr Zeit in Anspruch nehmen. Und wenn Sie einen Test, der durchschnittlich 50 Sekunden lang läuft, als klein markieren, bricht Ihr Test ab, wenn er auf einer Maschine mit einer alten CPU geplant wird. Daher sollten Sie für kleine Tests eine durchschnittliche Laufzeit von 30 Sekunden anstreben. Streben Sie für mittlere Tests eine durchschnittliche Laufzeit von 2 Minuten 30 Sekunden an.

### Reduzieren Sie die Anzahl der Proben und erhöhen Sie die Toleranzen für das Training

Langsam laufende Tests schrecken Mitwirkende ab. Das Lauftraining in Tests kann sehr langsam sein. Bevorzugen Sie höhere Toleranzen, um weniger Proben in Ihren Tests verwenden zu können, damit Ihre Tests ausreichend schnell sind (maximal 2,5 Minuten).

## Eliminieren Sie Nicht-Determinismus und Flocken

### Schreiben Sie deterministische Tests

Unit-Tests sollten immer deterministisch sein. Alle Tests, die auf TAP und Guitar ausgeführt werden, sollten jedes Mal auf die gleiche Weise ausgeführt werden, wenn keine Codeänderung sie beeinflusst. Um dies zu gewährleisten, sind im Folgenden einige Punkte zu beachten.

### Säen Sie immer jede Quelle von Stochastik

Jeder Zufallszahlengenerator oder jede andere Quelle von Stochastik kann Flockigkeit verursachen. Daher müssen diese jeweils ausgesät werden. Dies macht die Tests nicht nur weniger flockig, sondern auch alle Tests reproduzierbar. Es gibt verschiedene Möglichkeiten, einige Samen zu setzen, die Sie möglicherweise in TF-Tests setzen müssen:

```python
# Python RNG

import random
random.seed(42)

# Numpy RNG

import numpy as np
np.random.seed(42)

# TF RNG

from tensorflow.python.framework import random_seed
random_seed.set_seed(42)
```

### Vermeiden Sie die Verwendung von `sleep` in Multithread-Tests

Die Verwendung der `sleep` in Tests kann eine der Hauptursachen für Schuppen sein. Insbesondere wenn mehrere Threads verwendet werden, ist die Verwendung von sleep zum Warten auf einen anderen Thread nie deterministisch. Dies liegt daran, dass das System keine Reihenfolge der Ausführung verschiedener Threads oder Prozesse garantieren kann. Ziehen Sie daher deterministische Synchronisationskonstrukte wie Mutexe vor.

### Überprüfen Sie, ob der Test schuppig ist

Flakes führen dazu, dass Buildcops und Entwickler viele Stunden verlieren. Sie sind schwer zu erkennen und schwer zu debuggen. Obwohl es automatisierte Systeme zur Erkennung von Flockigkeit gibt, müssen sie Hunderte von Testläufen ansammeln, bevor sie Tests genau verweigern können. Selbst wenn sie es entdecken, verweigern sie Ihre Tests und die Testabdeckung geht verloren. Daher sollten Testautoren beim Schreiben von Tests überprüfen, ob ihre Tests flockig sind. Dies können Sie ganz einfach tun, indem Sie Ihren Test mit dem Flag `--runs_per_test=1000`

### Verwenden Sie TensorFlowTestCase

TensorFlowTestCase trifft die notwendigen Vorkehrungen wie das Seeding aller verwendeten Zufallszahlengeneratoren, um die Flakigkeit so weit wie möglich zu reduzieren. Wenn wir weitere Schwachstellenquellen entdecken und beheben, werden diese alle zu TensorFlowTestCase hinzugefügt. Daher sollten Sie TensorFlowTestCase verwenden, wenn Sie Tests für Tensorflow schreiben. TensorFlowTestCase wird hier definiert: `tensorflow/python/framework/test_util.py`

### Hermetische Tests schreiben

Hermetische Tests benötigen keine externen Ressourcen. Sie sind vollgepackt mit allem, was sie brauchen, und sie starten einfach alle gefälschten Dienste, die sie benötigen könnten. Alle anderen Dienste als Ihre Tests sind Quellen für Nicht-Determinismus. Selbst bei 99% Verfügbarkeit anderer Dienste kann das Netzwerk abbrechen, die RPC-Antwort kann sich verzögern und Sie erhalten möglicherweise eine unerklärliche Fehlermeldung. Externe Dienste können GCS, S3 oder eine beliebige Website sein, sind aber nicht darauf beschränkt.
