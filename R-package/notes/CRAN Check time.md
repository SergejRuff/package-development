
Siehe log-file.


Flavor: r-devel-windows-x86_64
Check: examples, Result: NA
  Examples with CPU (user + system) or elapsed time > 10s
            user system elapsed
  gem     433.18 186.54  619.82
  bag      27.39   0.52   28.14
  loop     25.14   0.27   25.41
  depmed   20.25   0.09   20.35
  hldepth  18.47   0.06   18.53

Flavor: r-devel-windows-x86_64
Check: Overall checktime, Result: NOTE
  Overall checktime 13 min > 10 min

-------

Your tests and the overall check need to be fast.
Otherwise the package wont be accepted.

---------
Lösung 1.  Schlechte Lösung.


Ich habe jetzt die Examples, die lange gedauert haben mit #-Symbolen markiert.

Das sind im Grunde dieselben Funktionen, die bereits in den letzten Fassungen  von RepeatedHighDim mit #-Symbolen markiert wurden.

ich habe auch die Anweisung aus den letzten Fassungen übernommen: ## Attention: calculation is currently time-consuming.

Jetzt laufen die Checks 45 Sekunden statt 10 Minuten. Das sollte also kein Problem sein.

Die anderen Probleme konnte ich auch lösen.

ich finde es aber natürlich schade, dass man #-Symbole nutzen muss. So sollten die Beispiele aber deutlich schneller laufen.

403 trat auf, weil die Seiten, die als Quelle benutzt wurden scheinbar nicht den Zugriff auf den Server erlaubten.

Ich habe jetzt stattdessen DOIs angegeben. Das sollte das Problem lösen.

Bei den anderen Quellen-Angaben wurde \url benutzt, dabei sollte es \doi sein, da es sich um DOI-Angaben handelte.


-----------------------------------------------

Bessere Lösung.

\dontrun{

Teil des Examples, der zu lange läuft.

}

Example from netmeta-package: https://github.com/guido-s/netmeta/blob/develop/R/netmeta.R

	![[Pasted image 20240405005617.png]]