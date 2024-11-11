1. Installation de pandoc : <http://pandoc.org/installing.html>

2. commandes à exécuter depuis le répertoire `Analyse_informatique_UML` pour générer les différents supports de cours :
    * Pour générer les slides :

    pandoc -s -t html5 --template=template\ign-ensg-revealjs.html --section-divs -o Analyse_informatique_presentation.html Analyse_informatique_presentation.md
    pandoc -s -t html5 --template=template\ign-ensg-revealjs.html --section-divs -o Analyse_avancee_presentation.html Analyse_avancee_presentation.md

    * Pour générer les pdf de cours :

    pandoc -s -N --listings --template=template\template.latex -o Analyse_informatique.pdf Analyse_informatique.md 
	pandoc -s -N --listings --template=template\template.latex -o Analyse_avancee.pdf Analyse_avancee.md 
	
    * Pour générer les pdf d'exercices :

    pandoc -s -N --listings --template=template\template_tp.latex -o Analyse_informatique_exercices.pdf Analyse_informatique_exercices.md 
    pandoc -s -N --listings --template=template\template_tp.latex -o Analyse_avancee_exercices.pdf Analyse_avancee_exercices.md 
