# Générer les pdf / présentations en html des supports de cours

1. Installation de pandoc : <http://pandoc.org/installing.html>
2. Se placer à la racine du répo
3. Pour générer les diapositives :
```shell
pandoc -s -t html5 --template=template/ign-ensg-revealjs.html --section-divs --variable revealjs-url="https://cdn.jsdelivr.net/npm/reveal.js@3.3.0" -o Analyse_informatique_presentation.html Analyse_informatique_presentation.md
pandoc -s -t html5 --template=template/ign-ensg-revealjs.html --section-divs --variable revealjs-url="https://cdn.jsdelivr.net/npm/reveal.js@3.3.0" -o Analyse_avancee_presentation.html Analyse_avancee_presentation.md
```

5. Pour générer les pdf de cours :
```shell
pandoc -s -N --listings --template=template/template.latex -o Analyse_informatique.pdf Analyse_informatique.md 
pandoc -s -N --listings --template=template/template.latex -o Analyse_avancee.pdf Analyse_avancee.md 
```

5. Pour générer les pdf d'exercices :
```shell
pandoc -s -N --listings --template=template/template_tp.latex -o Analyse_informatique_exercices.pdf Analyse_informatique_exercices.md 
pandoc -s -N --listings --template=template/template_tp.latex -o Analyse_avancee_exercices.pdf Analyse_avancee_exercices.md 
```
