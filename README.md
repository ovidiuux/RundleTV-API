# Rundle TV - Documentație API.
https://user-emea-api.rundletv.eu.org/

Salutări! 👋
Pentru a începe să foloseși API nostru ai nevoie de o cheie API la care o poți obține prin contanct la api@rundletv.eu.org

Hai, să începem autentificarea! Ai nevoie de chiea API și cheia secretă 🤫. Fiecare cheie este unică și este ca un ID pentru tine.
Este securizat prin jetoane (token-uri) și acestea expiră după un anumit interval și se pot folosi pentru a te putea autentifica la Rundle API.

Fiecare cheie API este în baza adresei URL, de exemplu: https://user-emea-api.rundletv.eu.org/content/da2c83a3cf655338929fb8522e329d95
Și este autentificarea principală, este sigur să o folosești oriunde.

Atenție, aici trebuie să fie undeva pe un server, nu în baza aplicației, aici se trimite cheia secretă 🤫
Pentru a începe să obți un jeton, trebuie să trimiți o cerere GET cu anumiți parametri:
URL: "http://user-emea-api.rundletv.eu.org/" + CHEIE_API + "/token"
Originea și referrer-ul pe care le-ai primit pe email de la api@rundletv.eu.org.
Și bineînțeles cheia secretă.

Exemplu, în PHP:

		<?php
		$url = "https://user-emea-api.rundletv.eu.org/content/da2c83a3cf655338929fb8522e329d95/token";

		$curl = curl_init($url);
		curl_setopt($curl, CURLOPT_URL, $url);
		curl_setopt($curl, CURLOPT_RETURNTRANSFER, true);

		$headers = array(
		   "rundle-secret: "d224bc5228293d4464d6ec76a13b6a4f163d0be7",
		   "origin": "https://site-ul-meu.ro",
		   "referrer": "https://site-ul-meu.ro/"
		);
		curl_setopt($curl, CURLOPT_HTTPHEADER, $headers);

		$resp = curl_exec($curl);
		curl_close($curl);
		echo json_encode($resp);

		?>


Exemplu, în Node.Js (cu Express.js)

    app.get(async (req, res) => {
    	const base = "https://user-emea-api.rundletv.eu.org/";
	const api_key = "da2c83a3cf655338929fb8522e329d95";
	const secret_key = "d224bc5228293d4464d6ec76a13b6a4f163d0be7";

	const rundleAPI = await fetch(base + api_key + "/token", {
	     headers: {
		"rundle-secret: secret_key,
		"origin": "https://site-ul-meu.ro",
		"referrer": "https://site-ul-meu.ro/"
	     }
	});

	const responseAPI = await rundleAPI.json();
	console.log(responseAPI);
     	res.send(responseAPI.token);
     }
