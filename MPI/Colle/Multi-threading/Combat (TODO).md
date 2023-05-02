On essaye de coder un serveur pour un jeu vidéo de combat.
Nous avons besoin du comportement suivant : 
 - Les joueurs se connecte à un lobby commun.
 - Quand une des $k$ arènes se libère, les $n$ joueurs prioritaires y sont envoyés.
 - Les joueurs quand ils perdent se déconnectent un à un de leur arène et retourne au lobby.

Chaque joueur sera représenté par un fil d’exécution.
Proposer une architecture utilisant des sémaphores pour implémenter.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1NzU1MjM3NzFdfQ==
-->