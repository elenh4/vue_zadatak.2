<script setup>
const slike = {
    Jabuka: "https://www.svgrepo.com/show/530203/apple.svg",
    Mrkva: "https://www.svgrepo.com/show/530216/carrot.svg",
    Sir: "https://www.svgrepo.com/show/530219/cake.svg",
    Kruh: "https://www.svgrepo.com/show/530223/bread.svg",
};

const proizvodi = [
    { naziv: "Jabuka", cijena: 0.25 },
    { naziv: "Mrkva", cijena: 0.12 },
    { naziv: "Kruh", cijena: 2.00 },
    { naziv: "Sir", cijena: 4.48 }
];

const korisnik = {
    jeAdmin: true,
    osobni_podaci: {
        ime: "Marko",
        prezime: "Krivić",
        adresa: {
            grad: "Pula",
            ulica: "Veruda",
            broj: 32
        },
        broj_telefona: "+091-123-456"
    },
    kosarica: [
        { naziv: "Jabuka", količina: 4 },
        { naziv: "Mrkva", količina: 12 },
        { naziv: "Kruh", količina: 3 },
        { naziv: "Sir", količina: 1 },
    ]
};

function dohvatiCijenu(naziv) {
    const proizvod = proizvodi.find(p => p.naziv === naziv);
    return proizvod ? proizvod.cijena : 0;
}

function sveukupnaCijena() {
    return korisnik.kosarica.reduce((total, item) => total + ukupno_stavke(item.naziv, item.količina), 0);
}

function najskupljaStavka() {
    const najskuplja = korisnik.kosarica.reduce((najskuplja, trenutna) => ukupno_stavke(trenutna.naziv, trenutna.količina) > ukupno_stavke(najskuplja.naziv, najskuplja.količina) 
        ? trenutna 
        : najskuplja
    );
    return najskuplja.naziv;
}
function ukupno_stavke(naziv, količina) {
    return dohvatiCijenu(naziv) * količina;
}
  
</script>

<template>
  <div class=" max-w-md mx-auto ">
    <div class="bg-blue-50 text-sky-600 h-38 w-120 rounded-lg  border-gray-300 border-1 ">
        <h1 :class="korisnik.jeAdmin ? 'text-sky-600' : 'text-black'" class="text-lg ml-6  font-bold mb-2 mt-4 " >Korisnički podaci</h1>

        <hr class="bg-sky-600 rounded-full ml-6 mr-20">

        <div class="ml-6 mt-2">
          <p :class="korisnik.jeAdmin ? 'text-sky-600' : 'text-black'"><span class="font-bold">Ime:</span> {{ korisnik.osobni_podaci.ime }} {{ korisnik.osobni_podaci.prezime }}</p>
          <p :class="korisnik.jeAdmin ? 'text-sky-600' : 'text-black'"><span class="font-bold" >Adresa:</span> {{ korisnik.osobni_podaci.adresa.ulica }} {{ korisnik.osobni_podaci.adresa.broj }}, {{ korisnik.osobni_podaci.adresa.grad }}</p>
          <p :class="korisnik.jeAdmin ? 'text-sky-600' : 'text-black'"><span class="font-bold" >Telefon:</span>{{ korisnik.osobni_podaci.broj_telefona }} </p>
          
        </div>
    </div>

    <div class="bg-blue-50 text-black-600 h-170 w-120 rounded-lg  mb-4 mt-4 border-gray-300 border-1 ">
      <h2 class="font-bold ml-6 text-2xl mb-2 mt-4 inline-flex">
        <img src="https://www.svgrepo.com/show/477342/shopping-cart-free-7.svg" 
             alt="Košarica" class="w-6 h-6 mr-2"> Košarica
      </h2>

      <div class="bg-blue-50 text-black-600 h-32 w-105 rounded-lg ml-6  border-gray-400 border-1 flex items-center" 
        :class="{'bg-red-50 border p-2 mb-4 rounded-lg border-red-300 ': korisnik.kosarica[0].naziv===najskupljaStavka()}">
        <img :src="slike.Jabuka"  class="w-20 h-20 rounded-lg">
        <p><span class="font-bold">Jabuka</span> 
        <ul>
           <p>Cijena: €{{ dohvatiCijenu(korisnik.kosarica[0].naziv) }} | Količina: {{ korisnik.kosarica[0].količina }}</p>
           <p>Ukupno: €{{ (dohvatiCijenu(korisnik.kosarica[0].naziv) * korisnik.kosarica[0].količina).toFixed(2) }}</p>               
        </ul>
        </p>
      </div>
     
      <div class="bg-blue-50 text-black-600 h-32 w-105 rounded-lg ml-6 border-gray-400 border-1 flex items-center mt-4"
        :class="{'bg-red-50 border p-2 mb-4 rounded-lg border-red-300 ': korisnik.kosarica[1].naziv===najskupljaStavka()}">
        <img :src="slike.Mrkva"  class="w-20 h-20 rounded-lg ">
        <p><span class="font-bold">Mrkva</span> 
        <ul>
           <p>Cijena: €{{ dohvatiCijenu(korisnik.kosarica[1].naziv) }} | Količina: {{ korisnik.kosarica[1].količina }}</p>
           <p>Ukupno: €{{ (dohvatiCijenu(korisnik.kosarica[1].naziv) * korisnik.kosarica[1].količina).toFixed(2) }}</p>               
        </ul>
        </p> 
      </div>

      <div class="bg-blue-50 text-black-600 h-32 w-105 rounded-lg ml-6 border-gray-400 border-1 flex items-center mt-4"
        :class="{'bg-red-50 border p-2 mb-4 rounded-lg border-red-300 ': korisnik.kosarica[2].naziv===najskupljaStavka()}">
        <img :src="slike.Kruh" class="w-20 h-20 rounded-lg">
        <p><span class="font-bold">Kruh</span>
        <ul>
           <p>Cijena: €{{ dohvatiCijenu(korisnik.kosarica[2].naziv) }} | Količina: {{ korisnik.kosarica[2].količina }}</p>
           <p>Ukupno: €{{ (dohvatiCijenu(korisnik.kosarica[2].naziv) * korisnik.kosarica[2].količina).toFixed(2) }}</p>               
        </ul>
        </p>
      </div>

      <div class="bg-blue-50 text-black-600 h-32 w-105 rounded-lg ml-6 border-gray-400 border-1 flex items-center mt-4"
        :class="{'bg-red-50 border p-2 mb-4 rounded-lg border-red-300 ': korisnik.kosarica[3].naziv===najskupljaStavka()}">
        <img :src="slike.Sir"  class="w-20 h-20 rounded-lg">
        <p><span class="font-bold">Jabuka</span> 
        <ul>
           <p>Cijena: €{{ dohvatiCijenu(korisnik.kosarica[3].naziv) }} | Količina: {{ korisnik.kosarica[3].količina }}</p>
           <p>Ukupno: €{{ (dohvatiCijenu(korisnik.kosarica[3].naziv) * korisnik.kosarica[3].količina).toFixed(2) }}</p>               
        </ul>
        </p>
      </div>

      <h2 class="font-bold ml-6 mt-2 text-lg">Ukupna cijena: <span class="font-light">€{{ sveukupnaCijena().toFixed(2) }}</span></h2>
    </div>

  
  </div>

</template>

<style scoped>

</style>
