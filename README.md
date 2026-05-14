// paramètres de simulation
const P = 3; // kWc
const autocons = 0.45;
const prix_kwh = 0.25; // €/kWh économisé
const r_oa = 0.13; // €/kWh vendu
const CAPEX = 6000; // €
const prime_auto = 370; // €/kWc
const degrad = 0.005; // 0,5%
const inflation = 0.02; // 2%
const annees_eval = 25;

let flux_total = 0;
for (let n = 1; n <= annees_eval; n++) {
  const prod_n = annual * Math.pow(1 - degrad, n - 1);
  const R_auto = prod_n * autocons * prix_kwh * Math.pow(1 + inflation, n - 1);
  const R_oa = prod_n * (1 - autocons) * r_oa;
  flux_total += R_auto + R_oa;
}

const prime = prime_auto * P;
const ROI = ((flux_total + prime - CAPEX) / CAPEX * 100).toFixed(1);
const payback = (CAPEX / (flux_total / annees_eval)).toFixed(1);

document.getElementById("result").innerHTML += `
  <hr>
  <p><b>Production annuelle :</b> ${annual} kWh</p>
  <p><b>Autoconsommation :</b> ${(autocons * 100)} %</p>
  <p><b>Revenus cumulés 25 ans :</b> ${(flux_total + prime).toFixed(0)} €</p>
  <p><b>ROI sur 25 ans :</b> ${ROI} %</p>
  <p><b>Retour sur investissement moyen :</b> ${payback} ans</p>
`;
