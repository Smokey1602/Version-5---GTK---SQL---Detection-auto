Bonjour,

Ce répertoire regroupe la version 5 du compteur. 
Cette version n'influence en rien le traitement video. il ajoute l'utilisation de la librairie SQL pour enrgistrer les fichiers sur un 
serveur distant. il est toutdefois possible d'utiliser cet ajout pour effectuer une sauvegarde sous un BBD interne a la raspberry / pc

Il garde les options de base:
  - Sauvegarde automatique toutes les minutes
  - Création et  sauvegarde d'un graphique
  - Interface graphique grace a opencv
  - Traitement video
  - Comptage
  
Et ajoute :
  - Gestion de la sauvegarde sous une BDD
  
Il suffit de compiler le fichier "camera.c" sous linux avec la librairie openCV pour essayer le programme
    g++ -Wall -o executable camera.c `pkg-config --cflags --libs opencv` `mysql_config --cflags --libs`
    
    
Pour modifier l'adresse du serveur changer votre IP cherchez cette trame sur le fichier.c et modifier la avec vos parametres. Cette ligne peut
etre trouvée dans la fonction "void sauvegarde_sql(void)"

    if(NULL == mysql_real_connect(mysql,"IP","USER","MOT_DE_PASSE","NOM_DE_LA_BDD",0,NULL,0))
    
Il faudra egalement modifier cette ligne dans les deux cas où elle apparait

sQLComplete = (char*)malloc(strlen("INSERT INTO NOM_DE_LA_TABLE(date,entree,sortie) VALUES('%s','%s','%s')")+40);
    
