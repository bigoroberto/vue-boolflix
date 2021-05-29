<!-- TUTTI I PASSAGGI IN ORDINE -->

<!-- (App.vue) Creo la funzione che mi fa chiamare l'API ogni volta che ne ho bisogno  -->

<!-- (App.vue) Creo la var alla quale assegno l' url dell' API e nella funzione passerò direttamente la var per sporcare di meno il codice  -->

<!-- (App.vue) La query la passo tramite le tonde della funzione dell'API -->

<!-- (App.vue) Adesso nell apiUrl togliamo il movie-->

<!--(App.vue) Aggiungo "type" dentro le tonde della funzione dopo la query così le concateniamo getAPI(query, type)  -->

<!-- (App.vue) Nell'axios.get dopo il this ulr aggiungiamo il type quindi 
axios.get(this.apiUrl + type, {  -->

<!-- Creo i componenti headere.vue e Main.vue, li inizializzo e li importo -->

<!-- (Header.vue) Creo l'input ed i bottoni -->

<!-- (Header.vue) Creo un v-model nell'input che conterrà il testo che andrò a cercare e lo inizializzo nel DATA come una var vuota-->

<!-- (Header.vue) Cliccando sul bottone faccio partire l'$emit (chiamerò l'evento "startSearch"-->

<!-- (Header.vue) Faccio tre bottoni , uno per la ricerca dei film, uno per le serie ed uno per il totale -->

<!-- (Header.vue) Al primo bottone gli dico "cercami il v-model, cercami il film " -->

<!-- (Header.vue) Passo l'infomazione all'$emit, un oggetto, quindi @click="$emit('startSearch', {text:textToSearch, type:'movie'})" così in questo modo al mio evento gli passo due informazioni, gli passo il testo da cercare ed il tipo di ricerca che devo fare -->

<!-- (Header.vue) Secondo bottone stessa metodo, sostituisco il 'movie'(che mi trova i film) nel type, con 'tv' ( che mi andrà a trovare le serie tv) -->

<!-- (Header.vue) Terzo bottone ancora stesso metodo, sostituisco il 'tv'(che mi da le serie tv) con 'all' (che mi darà entrambi i risultati) -->

<!--(App.vue) Metto in ascolto l'$emit nel template aggiungo il nome dell'evento all'Header, quindi "startSearch" e gli aggiungo un valore che chiamerò come il nome dell'$emit. 
<Header @startSearch="startSearch" /> -->

<!-- (App.vue) Nei metodi vado a creare una funzione startSearch che ho abbinato all'evento dell'$emit, nelle tonde della funzione avrà come parametro l'oggetto che abbiamo attribuito all'$emit nell'Header.vue quindi:
startSearch(obj){   -->

<!-- (App.vue) Adesso nella funzione starSearch faccio un filtro, detto una condizione, gli dico che se obj.type è all faccio entrambe le chiamate, altrimenti gli passo esattamente la chiamata che devo fare. quindi: 
startSearch(obj){
  if(obj.type ==='all'){
    this.getAPI(obj.text, 'movie');
    this.getAPI(obj.text, 'tv'); 
    }else{
      this.getAPI(obj.text, obj.type);
      }
    }, 
-->

<!-- (Main.vue) Creo entrambi i titoli, e poi come props mi arriva l'informazione è movie o è tv, stampo un titolo o stampo l'altro di conseguenza se io mi faccio un oggetto , che chiamerò titles che se è movie è film trovati e se è tv è serie tv trovate . quindi:
data(){
  return{
    titles:{
      'movie':'Film trovati'
      'tv': 'Serie tv trovate'
      }
    }
  },
-->

<!-- (Main.vue) Preparo una props che chiamerò type che è una stringa 
  props:{
    type:String
    },
-->

<!--(Main.vue) Quando mi arriverà la props io stampo l'oggetto titles ed il type,   nell'h1 in modo dinamico. con il type quando sarà movie mi stamperà movie e quando sarà tv mi stamperà tv
<h1>{{titles[type]}}</h1>
-->

<!-- (App.vue) Ho la gestione dei titoli quindi ora nel teplate creo due <Main /> ad uno stampo il type='movie' e nell'altro il type='tv'
<Main type='movie' />
<Main type='tv' />
-->

<!-- (App.vue) Creo un oggetto in DATA che chiamo results che ha due proprietò, una 'movie' che è un array e 'tv' che è un array,

  data(){
    return{
      apiUrl: 'https://api.themoviedb.org/3/search/',
      apiKey: '883d759bdcf64cac4dd1122ba345f4b3',
      query: '',
      results:{
        'movie':[],
        'tv':[],
      }
    }
  },
-->

<!-- (App.vue) Quando mi arriva il dato dalla chiama API, nel then della funzione getAPI, prendo il risultato e lo metto nel results aggiungendo anche il type
      .then(res=>{
        this.results[type] = res.data.results
        console.log(this.results);
      })
-->

<!-- (App.vue) Faccio una funzione nei methods che mi resetti le chiamate che chiamerò resetResults
  resetResults(){
    this.result.movie = [];
    this.result.tv = [];
  }
-->

<!-- (App.vue) Aggiungo la funzione appena creata all'interno della funzione startSearch così resetto tutto all'inizio così non sbaglio, ogni volta resetto e faccio la mia ricerca 

starSearc(obj){
  this.resetResults();
  if(obj.type === 'all'){
    this.getAPI(obj.text , 'movie');
    this.getAPI(obj.text , 'tv');
  }else{
    this.getAPI(obj.text, obj.type);
  }
},
-->

<!--(App.vue) Faccio un v-if nel template dei Main e gli dico che se l'array di movie è maggiore di 0 me lo stampa, stessa cosa per l'altro main nel template. in più gli passo un oggetto list che andrà bindato

<Main v-if="results.movie.length > 0" type='movie' :list="results.movie" /> 

<Main v-if="results.tv.length > 0" type='tv' :list="results.tv" /> 
-->

<!-- (Main.vue) Creo un props che mi accolga la list mandata dal padre APP.VUE  e gli dico che list è un array

props:{
  list:Array
-->


<!--Creo un nuovo componente che chiamerò Card.vue per stamapre a video la inizializzo e la importo dove mi serve, in questo caso mi serve nel main quindi l'import lo farò nel MAIN.VUE, la richiamo nel template e l'aggiungo ai components-->

<!--(Main.vue) Faccio un v-for della Card nel template-->

<!--(Main.vue) A questo punto gli passo la card che è un oggetto
<Card
  v-for="card in list"
  :key"card.id"
  :card="card"
  />
-->

<!--(Card.vue) Preparo a ricevere l'oggetto quindi
props:{
  card:Object
}
-->

<!--(Card.vue) Stampo a video quello richiesto ovvero il titolo, titolo originale, lingua  -->

<!--(Card.vue) Carico la lista da bootstrap nella quale andrò ad inserire dentro gli LI ciò che mi serve
<ul class="list-group">
  <li class="list-group-item">{{card.title}}</li>
  <li class="list-group-item">{{card.original_title}}</li>
  <li class="list-group-item">{{card.original_language}}</li>
  <li class="list-group-item">{{card.vote_average}}</li>
</ul>
-->


<!-- -->
<!-- -->
<!-- -->
<!-- -->
<!-- -->