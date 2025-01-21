# Sentimentanalyse-Fiskalpolitischer-Wirtschaftsartikel

Der hier hochgeladene Code diente als Grundlage für meine Bachelorarbeit an der TU Darmstadt. Im Rahmen dieser Arbeit habe ich Artikel des Handelsblatts mit einem Bezug zur deutschen Fiskalpolitik auf mögliche Voreingenommenheit in der Berichterstattung untersucht. Hierbei kamen vor allem Techniken aus dem Bereich des Natural Language Processing (NLP) zum Einsatz, insbesondere Sentimentanalysen.

## daten
Der Ordner enthält die für die Sentimentanalysen verwendeten Wörterbücher, die Liste an spezifischen Stoppwörtern sowie die ermittelten Sentimententwicklungen in Artikeln des Handelsblatts und Bundestagsreden.

Den gesamten Datensatz an Wirtschaftsartikeln (insgesamt wurden in dieser Arbeit über 23.000 Artikel analysiert) darf ich hier nicht hochladen.

## 01 Vorbereitung der Textdaten
Sowohl der Datensatz der Wirtschaftsartikel als auch der der Bundestagsreden musste vor der Sentimentanalyse bereinigt werden. Das Vorgehen zur Datenaufbereitung war für beide Datensätze weitgehend ähnlich. Im Gegensatz zu den Bundestagsreden, die bereits von Latifi et al., (2024) in strukturierter Form bereitgestellt wurden ([siehe hier](https://github.com/albi-lt/Fiscal-Policy-in-the-Bundestag/blob/main/README.md)), mussten die Artikel vor der Bereinigung zunächst in eine geordnete Form überführt werden.

Zusätzlich wurden das LNTW-Wörterbuch sowie die spezifische Liste von Stoppwörtern, die ebenfalls über das genannte Repository verfügbar sind, angepasst, um den Anforderungen dieser Arbeit gerecht zu werden.

Zur Vorbereitung der Textdaten gehörte:
1. Lemmatisieren des Texts
2. Umlaute umwandeln
3. Sonderzeichen und Bindestriche entfernen
4. Standard nltk-Stoppwörter entfernen
5. Spezifische Stoppwörter entfernen

## 02 Sentiment bestimmen
Für die Bestimmung des Sentiments wurden einerseits das Wörterbuch von Latifi et al., (2024) sowie das BPW Wörterbuch von Bannier et al., (2019) ([siehe hier](https://www.uni-giessen.de/de/fbz/fb02/forschung/research-networks/bsfa/textual_analysis/index)) angepasst und auf den Korpus angewendet. Die angepassten Wörterbücher werden in dieser Arbeit als LNTWS- und BPWS-Wörterbuch bezeichnet.

Das LNTWS-Wörterbuch, das speziell für den fiskalpolitischen Kontext entwickelt wurde, ermöglicht eine Einteilung des Sentiments in expansiv und restriktiv. Es enthält separate Listen von Begriffen, die entweder expansiv oder restriktiv konnotiert sind. Dabei wurde das Wörterbuch insbesondere dahingehend angepasst, dass es eindeutige Bigramme umfasst, um den fiskalpolitischen Kontext besser erfassen zu können.
Im Gegensatz dazu ist das BPWS-Wörterbuch in positiv und negativ konnotierte Begriffe unterteilt. Es basiert ausschließlich auf Unigrammen und berücksichtigt daher den Kontext der relevanten Wörter nicht.

Das LNTWS-Sentiment in den Artikeln wurde anschließend mit der prozentualen Veränderung des BIPs verglichen, während das BPWS-Sentiment mit dem ifo-Geschäftsklimaindex verglichen wurde.

## 03 Vergleich des Sentiments in Artikeln und Reden
Um zu ermitteln, ob die Autoren des Handelsblatts im Vergleich zu den Rednern des deutschen Bundestages eine tendenziell expansivere/restriktivere oder positivere/negativere Einstellung aufweisen, wird das Sentiment in den Artikeln mit dem Sentiment in den Bundestagsreden verglichen. Darüber hinaus wird in diesem Abschnitt die Korrelation zwischen den Datensätzen untersucht, einschließlich ihrer Beziehung zum Bruttoinlandsprodukt (BIP) und dem ifo-Geschäftsklimaindex. Ziel ist es, eine umfassende Korrelationsmatrix aller Datensätze zu erstellen.

## 04 Affinität zu einer Partei
Zusätzlich wurde untersucht, ob die Stimmung einer bestimmten Partei in den Artikeln besonders aufgegriffen und adaptiert wird. Dazu wurde ermittelt, welche Partei das ähnlichste BPWS-Sentiment zu den Artikeln aufweist. Ergänzend wurde mithilfe eines TF-IDF-Ansatzes analysiert, zu welcher Partei die Wortwahl in den Artikeln am ähnlichsten ist. Hierfür wurden zunächst die TF-IDF-Werte aller Terme in den Artikeln und Reden berechnet und anschließend pro Jahr sowie für die Reden zusätzlich nach Parteien aggregiert. Auf dieser Basis wurde die Ähnlichkeit der Wortwahl mithilfe der Kosinus-Ähnlichkeit bestimmt.
