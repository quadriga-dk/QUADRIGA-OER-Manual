(entwicklung:einleitung)=
# Entwicklungsumgebung

Für jede QUADRIGA OER, die als Jupyter Book entwickelt wird, sollte die automatische Erstellung der Website per GitHub Actions aktiviert sein. Dadurch werden Änderungen im Haupt-Entwicklungsstrang (`main`-branch in Git) automatisch gebaut, wenn sie in GitHub veröffentlicht werden. Kleinere Änderungen wie bspw. die Behebung von Tippfehlern können daher sogar über die Web-Oberfläche von GitHub getätigt werden. Größere Änderungen und die experimentelle (und ggf. private) Weiterentwicklung benötigen jedoch eine lokale Entwicklungsumgebung. Empfehlungen dazu, wie Sie diese bei sich einrichten können, werden in den nachfolgenden Abschnitten beschrieben.

Das <a href="https://github.com/quadriga-dk/Book_Template" class="external-link" target="_blank"><code>Book_Template</code></a> bringt dafür bereits eine passende GitHub Action und eine vollständige Projektstruktur mit. Sie starten also nicht bei Null, sondern ergänzen und verändern eine vorhandene Einrichtung. Diese Anleitung erklärt, was die einzelnen Bestandteile tun und wie Sie sie für Ihre OER anpassen.

## Bestandteile der Entwicklungsumgebung
Die Entwicklungsumgebung besteht aus verschiedenen Software-Komponenten. Diese sind Git, eine Python-Distribution sowie Jupyter Book und andere Python-Programmbibliotheken, die in der OER genutzt werden sollen. Werden andere Programmiersprachen wie bspw. R genutzt, so müssen diese und alle nötigen Programmbibliotheken zusätzlich in der lokalen Umgebung (und in der GitHub Action) vorhanden sein.

Konkret benötigen Sie:
- Git, um die Versionsverwaltung durchzuführen und um mit GitHub zu interagieren;
- Python – vorzugsweise über die Anaconda Distribution –, um Jupyter Book lokal nutzen zu können und ggf. für Inhalte der OER;
- Jupyter Book, um während des Schreibens lokal die Markdown-Dateien und Jupyter Notebooks in eine Website-Ansicht zu transformieren;
- sowie ggf. ein Editor oder eine IDE wie VSCode, wenn die Bearbeitung der Dateien nicht über die Jupyter Notebook- oder Jupyter Lab-Oberfläche aus der Anaconda Distribution erfolgen soll;
- und ggf. eine grafische Oberfläche für Git wie GitHub Desktop.

## Aufbau dieses Kapitels
Dieses Kapitel stellt Ihnen nach der Einleitung kurz die einzelnen Software-Komponenten vor und gibt dann jeweils Hinweise zur Installation und der Nutzung der jeweiligen Software. Im Anschluss wird der ganzheitliche Ablauf und das Zusammenspiel der einzelnen Software für die Entwicklung der QUADRIGA OER beispielhaft dargestellt.

