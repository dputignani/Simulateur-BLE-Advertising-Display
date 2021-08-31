Simulateur Ecran vélo Bluetooth

But de ce simulateur : Le but de ce simulateur est d’offrir un moyen de test pour développer la test APP pour le premier livrable : Advertising et connexion notamment : pour tester le processus de bonding souhaité par Decathlon, ainsi que pour récupérer les informations advertising souhaités par Decathlon, la partie Whitelisting est implémentée ici mais DPE (fournisseur)  rencontre des problèmes pour l’implémenter actuellement sur le produit final, le produit final se comportera donc peut-être différemment à ce niveau-là. 
Comportement de la carte : 
Lors d’un démarrage usine, le système advertise pas (whiteliste vide)
Un appuie long sur le bouton 4 permet d’advertiser et d’accepter un nouveau téléphone
Le système rejette les demandes de connexion de téléphone non enregistrés
Le système advertise pendant 30 s
Une déconnexion refait passer le système en mode advertising pendant 30s

La trame d’advertising est composée de la sorte : 
[Length=6][type=Complete_Local_Name]["EB100"]
[length=2][type= Flag][FLAG_LE_LIMITED_DISC_MODE]
[Length=16][Type=manufacturer_Data][ID_Decathlon][bonding_state][“rockrider500”]
[Length =3][Type=appearance][cycling_computer]
Si [bonding_state] = 1 bonding autorisé, whitelist désactivée
Si [bonding_state] = 0 bonding non autorisé, whitelist activée
(ID_Decathlon = 0xFFFF en attendant d’en avoir un officiel)

Action sur les boutons: 
Un appuie sur le bouton 2 + sur le bouton reset :
Ça supprime les informations de bonding (les téléphones en mémoire)
Un appuie long (>1s) sur le bouton 4 : 
Si aucun téléphone n’est enregistré ou Si le système est passé en mode IDLE 
ça démarre l’advertising et autorise le bonding
Si au moins un téléphone est enregistré ET le système advertise, ça désactive momentanément la whitelist pour qu’on puisse faire le bonding d’un nouveau téléphone

Etat des Leds :
Led 1 est éteinte : système IDLE (soit on a atteint les 3 min d’advertising, soit la whiteliste est vide et on n’autorise pas l’advertising)
Led 1 clignote lentement : Advertise, Whitelist désactivée, bonding d’un nouveau téléphone autorisé
Led 1 clignote rapidement : Advertise, Whitelist active, connexion avec un nouveau téléphone rejeté 
Note : Lors d’une connexion, le bonding est automatiquement demandé du produit vers le téléphone (pop-up system), si le téléphone/ l’utilisateur refuse le produit se déconnecte.

Mise à jour simulateur : 
Télécharger nrf_connect pour le bureau, puis sélectionner « Programmer », add HEX file & sélectionner les 2 fichiers reçu de Decathlon, sélectionner la carte dans la liste & flasher (erase & write).
