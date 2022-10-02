#!/usr/bin/python
de __future__ importer print_function
de l'import mathématique *
importer au hasard
importer système
importer numpy en tant que np
importer l'heure en tant que pytime
importer matplotlib.pyplot en tant que plt
__auteur__ = "Dominique Delande"
__copyright__ = "Copyright (C) 2017 Dominique Delande"
__license__ = "GPL version 2 ou ultérieure"
__version__ = "1.0"
#
# Ce programme est un logiciel gratuit ; vous pouvez le redistribuer et/ou le modifier
# selon les termes de la licence publique générale GNU telle que publiée par
# la Fondation du logiciel libre ; soit la version 2 de la Licence, soit
# (à votre choix) toute version ultérieure.
#
# Ce programme est distribué dans l'espoir qu'il sera utile,
# mais SANS AUCUNE GARANTIE ; sans même la garantie implicite de
# QUALITÉ MARCHANDE ou ADAPTATION À UN USAGE PARTICULIER. Voir le
# Licence publique générale GNU pour plus de détails.
#
# Vous devriez avoir reçu une copie de la licence publique générale GNU
# avec ce programme ; sinon, voir <http://www.gnu.org/licenses/>.
# _______________________________________________________________________
# Calcule plusieurs "trajectoires" de la carte standard
# Les conditions initiales sont générées aléatoirement
# Imprime les points dans le plan (theta,I) (modulo 2*pi)
# Matplotlib est utilisé pour visualiser les tracés
# De plus, les points sont imprimés dans le fichier "classical_trajectories.dat"
# Les trajectoires consécutives sont séparées par une ligne vide
# Seuls les points d'une zone restreinte sont réellement imprimés. Cela fait
# il est possible de zoomer dans une région limitée de l'espace des phases
# Il est possible d'éviter de remplir les disques en commentant
# la ligne "print(theta,I,file=f)" vers la fin
# _______________________________________________________________________

ppp=2.0*pi

if ((len(sys.argv)!=4) et (len(sys.argv)!=8)):
  print('Usage (3 [or 7] parameters):\n kicked_rotor_classical_trajectories.py K number_of_trajectories number_of_points [theta_min theta_max I_min I_max]')
  sys.exit()
K = float(sys.argv[1])
nombre_de_trajectoires = int(sys.argv[2])
nombre_de_points = int(sys.argv[3])
si (len(sys.argv)==8):
  theta_min=float(sys.argv[4])
  theta_max=float(sys.argv[5])
  I_min=float(sys.argv[6])
  I_max=float(sys.argv[7])
autre:
  theta_min=0.
  theta_max=dpi
  I_min=0.
  I_max=dpi
    

# Les valeurs suivantes pour les parcelles primaires
# Le temps d'exécution est insignifiant
#K=0.1, 0.5, 1.0, 2.0, 5.0, 8.0
# nombre_de_trajectoires=100
# nombre_de_points=1000


# Les valeurs suivantes sont bonnes pour un îlot secondaire
# Le temps d'exécution est insignifiant
#K=1.0
# nombre_de_trajectoires=200
# nombre_de_points=1000
# thêta_min=1.7
# theta_max=4.6
# I_min=2.5
# I_max=3.8

# Les valeurs suivantes sont bonnes pour un îlot ternaire
# Temps d'exécution environ 10 secondes
#K=1.0
# nombre_de_trajectoires=1000
# nombre_de_points=10000
# thêta_min=4.05
# theta_max=4.35
# I_min=3.6
# I_max=3.75

tab_theta=np.zeros(nombre_de_points)
tab_I=np.zeros(nombre_de_points)
f=open('trajectoires_classiques.dat','w')
print('# Données générées le',pytime.asctime(),file=f)
print('# Plusieurs trajectoires de la carte standard, pliées dans le carré [0,2*pi]x[0,2*pi]',file=f)
print('# K =',K,fichier=f)
print('# nombre_de_trajectoires =',nombre_de_trajectoires,fichier=f)
print('# nombre_de_points =',nombre_de_points,fichier=f)
print('# theta dans la plage de',theta_min,' à',theta_max,file=f)
print('# I dans la plage de',I_min, ' à',I_max,fichier=f)
plt.axis([theta_min,theta_max,I_min,I_max])
plt.xlabel(r'$\theta$',fontsize=20)
plt.ylabel('I',fontsize=20)
pour i_traj dans la plage (nombre_de_trajectoires) :
  thêta=aléatoire.uniforme(0,dpi)
  I=aléatoire.uniforme(0,dpi)
  j=0
  pour i dans la plage (nombre_de_points) :
    si ((theta>theta_min)&(theta<theta_max)&(I>I_min)&(I<I_max)):
      print(thêta,je,fichier=f)
      tab_theta[j]=thêta
      tab_I[j]=I
      j+=1
# Les deux lignes suivantes sont au cœur du calcul...
    I=(I+K*sin(thêta))%dpi
    thêta=(thêta+I)%dpi
  imprimer(' ',fichier=f)
  plt.plot(tab_theta[0:j],tab_I[0:j],linestyle='Aucun',marker='.',markersize=1)
f.close()
plt.show()
