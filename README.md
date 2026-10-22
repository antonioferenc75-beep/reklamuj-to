
<!DOCTYPE html>
<html lang="cs">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Reklamuj to</title>
<style>
body{font-family:Arial,sans-serif;background:#f3f5f8;color:#182230;margin:0;padding:20px}
main{max-width:650px;margin:auto}
header,section{background:white;padding:22px;border-radius:16px;margin-bottom:16px}
h1{font-size:32px;margin:0 0 10px}
p{line-height:1.6}
select,textarea,button{box-sizing:border-box;width:100%;padding:14px;margin-top:12px;border-radius:9px;font-size:16px}
select,textarea{border:1px solid #ccd2dc}
textarea{min-height:190px}
button{background:#175cd3;color:white;border:0;font-weight:bold}
a{color:#175cd3}
small{color:#667085}
</style>
</head>
<body>
<main>
<header>
<h1>Reklamuj to</h1>
<p>Pomůžeme ti připravit zprávu pro prodejce. Jednoduše, zdarma a česky.</p>
</header>
<section>
<h2>Co potřebuješ řešit?</h2>
<label for="problem">Vyber situaci</label>
<select id="problem">
<option value="reject">Prodejce mi zamítl reklamaci</option>
<option value="delay">Na reklamaci stále čekám</option>
<option value="delivery">Objednávka mi nedorazila</option>
</select>
<label for="details">Doplň podrobnosti</label>
<textarea id="details" placeholder="Např. název zboží, datum nákupu nebo číslo objednávky"></textarea>
<button onclick="generate()">Vytvořit návrh zprávy</button>
<textarea id="result" placeholder="Zde se zobrazí návrh zprávy..." aria-label="Návrh zprávy"></textarea>
<button onclick="copyText()">Zkopírovat zprávu</button>
<p id="notice" aria-live="polite"></p>
</section>
<section>
<h2>Užitečné odkazy</h2>
<p><a href="https://www.coi.cz/" target="_blank" rel="noopener">Česká obchodní inspekce (ČOI)</a></p>
<p><a href="https://coi.gov.cz/informace-o-adr/" target="_blank" rel="noopener">Mimosoudní řešení spotřebitelských sporů</a></p>
<small>Nástroj poskytuje obecné informace a návrhy textů, nikoli právní poradenství. Výsledek sporu nezaručuje.</small>
</section>
</main>
<script>
function generate(){
const p=document.getElementById('problem').value;
const d=document.getElementById('details').value.trim();
const opening={
reject:'Žádám o vysvětlení důvodů zamítnutí reklamace a o zaslání odůvodnění včetně podkladů, ze kterých jste vycházeli.',
delay:'Prosím o informaci o aktuálním stavu reklamace a o sdělení, jakým způsobem a kdy bude vyřízena.',
delivery:'Žádám o prověření nedoručené objednávky a o informaci, kdy bude doručena, případně jak navrhujete situaci vyřešit.'
};
document.getElementById('result').value=
'Dobrý den,\n\n'+opening[p]+'\n\nPodrobnosti:\n'+(d||'[Doplňte podrobnosti nákupu nebo reklamace]')+'\n\nProsím o písemnou odpověď.\n\nDěkuji.\nS pozdravem';
document.getElementById('notice').textContent='Návrh je připraven. Před odesláním zkontroluj údaje.';
}
async function copyText(){
const t=document.getElementById('result');
if(!t.value){document.getElementById('notice').textContent='Nejdřív vytvoř návrh zprávy.';return}
t.select();
try{await navigator.clipboard.writeText(t.value);document.getElementById('notice').textContent='Zpráva zkopírována.'}
catch(e){document.getElementById('notice').textContent='Text označ a zkopíruj ručně.'}
}
</script>
</body>
</html>
