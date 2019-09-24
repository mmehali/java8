# SSO 
1) l'utilisateur veut acceder à app1.com pour la premiere fois. 
   comme il n'est pas authentifie, un bouton de login est disponible. 
   lorsque celui-ci clique sur ce boutton il est redirigé vers le server SSO.
2) Le serveur SSO affiche une page de login, l'utilisateur rentre se identifiants. 
   le serveur SSO valide les identifiants et genere une token SSO. 
   Le serveur SSO enregistre le token SSO dans une cookie pour des future tentative 
   de login de l'utilisateur.
3) Le serveur SSO redirecte l'utilisateur vers app1.com. Dans l'url de redirection il ajout le token SSO en queryParam.
4) app1.com enregistre le token dans une cookie et change la vue pour l'utlisateur logué. 
   app1.com peut obtenir des informations de l'utilisateur soit en invoquant le serveur SSO 
   ou recuperer ces information a partir du token si celui-ci est un JWT token.
   
5) Maintenant, le même utilisateur tente d'acceder a app2.com. 
   Comme une application ne peut acceder qu'aux cookies  qui ont 
   le meme "origin" elle ne peut pas savoir que l'utilisateur est logué sur app1.com. 
   Donc l'utilisateur, doit toujours voir le boutton de login sur app2.
6) L'utilisateur clique sur le boutton et il est rediriger vers le SSO server. 
   le serveur SSO voie qu'il a une cookie, alors il redirige l'utilisateur vers app2.com avec le token SSO dans l'url (queryParam)
7) app2.com enregistre le token dans une cookie et change sa vue pour l'utilisateur logue.

At the end of this process there will be three cookies set in the user browser each for app1.com, app2.com, 
and login.example.com domains.
