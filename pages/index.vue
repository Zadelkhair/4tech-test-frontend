<template>
  <!-- listing of vehicles -->
  <div class="app container flex mx-auto mt-3">
    <button class="show-button" @click="showSideBar">
      <svg
        version="1.1"
        id="Layer_1"
        xmlns="http://www.w3.org/2000/svg"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        x="0px"
        y="0px"
        viewBox="0 0 300.906 300.906"
        style="enable-background: new 0 0 300.906 300.906"
        xml:space="preserve"
      >
        <g>
          <g>
            <path
              d="M288.953,0h-277c-5.522,0-10,4.478-10,10v49.531c0,5.522,4.478,10,10,10h12.372l91.378,107.397v113.978
			c0,3.688,2.03,7.076,5.281,8.816c1.479,0.792,3.101,1.184,4.718,1.184c1.94,0,3.875-0.564,5.548-1.68l49.5-33
			c2.782-1.854,4.453-4.977,4.453-8.32v-80.978l91.378-107.397h12.372c5.522,0,10-4.478,10-10V10C298.953,4.478,294.476,0,288.953,0
			z M167.587,166.77c-1.539,1.809-2.384,4.105-2.384,6.48v79.305l-29.5,19.666V173.25c0-2.375-0.845-4.672-2.384-6.48L50.585,69.531
			h199.736L167.587,166.77z M278.953,49.531h-257V20h257V49.531z"
            />
          </g>
        </g>
        <g></g>
        <g></g>
        <g></g>
        <g></g>
        <g></g>
        <g></g>
        <g></g>
        <g></g>
        <g></g>
        <g></g>
        <g></g>
        <g></g>
        <g></g>
        <g></g>
        <g></g>
      </svg>
      Filters
    </button>
    <div class="app-side-bar">
      <button class="hide-button" @click="hideSideBar">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="1.5"
          stroke="currentColor"
          class="w-6 h-6"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M6 18L18 6M6 6l12 12"
          />
        </svg>
      </button>
      <div class="app-side-bar-container">
        <h1 class="title">Filter ma recherche</h1>

        <div class="filter-section toggles">
          <!-- pretAPartir -->
          <div
            class="filter-item w-full"
            :class="{ active: filters.pretAPartir }"
          >
            <div class="flex items-center w-full">
              <label class="label">Pret a partir</label>
              <div class="flex items-center ml-auto">
                <ToggleInput
                  v-model="filters.pretAPartir"
                  :scale="0.8"
                  :colors="['#3c7381', '#3c7381']"
                />
              </div>
            </div>
          </div>

          <!-- zeroKm -->
          <div class="filter-item w-full" :class="{ active: filters.zeroKm }">
            <div class="flex items-center w-full">
              <label class="label">Zero Km</label>
              <div class="flex items-center ml-auto">
                <ToggleInput
                  v-model="filters.zeroKm"
                  :scale="0.8"
                  :colors="['#3c7381', '#3c7381']"
                />
              </div>
            </div>
          </div>

          <!-- promotions -->
          <div
            class="filter-item w-full"
            :class="{ active: filters.promotions }"
          >
            <div class="flex items-center w-full">
              <label class="label">Promotions</label>
              <div class="flex items-center ml-auto">
                <ToggleInput
                  v-model="filters.promotions"
                  :scale="0.8"
                  :colors="['#3c7381', '#3c7381']"
                />
              </div>
            </div>
          </div>
        </div>

        <div class="filter-section">
          <h3 class="title">Budget</h3>

          <div class="filter-item w-full">
            <ChoicesInput
              v-model="filters.budgetType"
              :choices="['Total', 'Mensuel']"
              :colors="['#004a5d', 'white']"
            />
          </div>

          <div class="filter-item w-full">
            <BetweenInput
              v-model="filters.between"
              :max="filters.betweenMax"
              :min="filters.betweenMin"
              :unit="'€'"
              :colors="['#004a5d', '#3c7381']"
            />
          </div>
        </div>

        <div class="filter-section filter-section-collapse">
          <button class="collapse-btn flex justify-between w-full">
            <h3 class="title">Marque</h3>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              class="w-6 h-6"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M19.5 8.25l-7.5 7.5-7.5-7.5"
              />
            </svg>
          </button>
          <!-- group of radio buttons ( Toutes, Citroën, Ford, Nissan, Suzuki, Dacia, Nissan, Renault ) -->
          <div class="filter-item">
            <input
              type="radio"
              name="marque"
              id="toutes"
              value="toutes"
              v-model="filters.marque"
            />
            <label for="toutes">Toutes</label>
          </div>

          <div class="filter-item">
            <input
              type="radio"
              name="marque"
              id="citroen"
              value="citroen"
              v-model="filters.marque"
            />
            <label for="citroen">Citroën</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="marque"
              id="ford"
              value="ford"
              v-model="filters.marque"
            />
            <label for="ford">Ford</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="marque"
              id="nissan"
              value="nissan"
              v-model="filters.marque"
            />
            <label for="nissan">Nissan</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="marque"
              id="suzuki"
              value="suzuki"
              v-model="filters.marque"
            />
            <label for="suzuki">Suzuki</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="marque"
              id="dacia"
              value="dacia"
              v-model="filters.marque"
            />
            <label for="dacia">Dacia</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="marque"
              id="nissan"
              value="nissan"
              v-model="filters.marque"
            />
            <label for="nissan">Nissan</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="marque"
              id="renault"
              value="renault"
              v-model="filters.marque"
            />
            <label for="renault">Renault</label>
          </div>
        </div>

        <div class="filter-section filter-section-collapse">
          <button class="collapse-btn flex justify-between w-full">
            <h3 class="title">Type de vehicule</h3>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              class="w-6 h-6"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M19.5 8.25l-7.5 7.5-7.5-7.5"
              />
            </svg>
          </button>

          <!-- group of radio buttons ( Citadine, Berline, Break, SUV / 4x4, Monospace / Ludospace, Coupe / Cabriolet ) -->
          <div class="filter-item">
            <input
              type="radio"
              name="type"
              id="toutes-type"
              value="toutes"
              v-model="filters.type"
            />
            <label for="toutes-type">Toutes</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="type"
              id="citadine"
              value="citadine"
              v-model="filters.type"
            />
            <label for="citadine">Citadine</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="type"
              id="berline"
              value="berline"
              v-model="filters.type"
            />
            <label for="berline">Berline</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="type"
              id="break"
              value="break"
              v-model="filters.type"
            />
            <label for="break">Break</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="type"
              id="suv"
              value="suv"
              v-model="filters.type"
            />
            <label for="suv">SUV / 4x4</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="type"
              id="monospace"
              value="monospace"
              v-model="filters.type"
            />
            <label for="monospace">Monospace / Ludospace</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="type"
              id="coupe"
              value="coupe"
              v-model="filters.type"
            />
            <label for="coupe">Coupe / Cabriolet</label>
          </div>
        </div>

        <div class="filter-section filter-section-collapse">
          <button class="collapse-btn flex justify-between w-full">
            <h3 class="title">Modele</h3>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              class="w-6 h-6"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M19.5 8.25l-7.5 7.5-7.5-7.5"
              />
            </svg>
          </button>

          <!-- C3
          Duster
          JUKE
          Puma
          Sx4 S-cross -->

          <!-- group of radio buttons ( Clio, Captur, Kadjar, Koleos, Mégane, Scénic, Trafic ) -->
          <div class="filter-item">
            <input
              type="radio"
              name="modele"
              id="toutes-modele"
              value="toutes"
              v-model="filters.modele"
            />
            <label for="toutes-modele">Toutes</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="modele"
              id="c3"
              value="c3"
              v-model="filters.modele"
            />
            <label for="c3">C3</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="modele"
              id="duster"
              value="duster"
              v-model="filters.modele"
            />
            <label for="duster">Duster</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="modele"
              id="juke"
              value="juke"
              v-model="filters.modele"
            />
            <label for="juke">JUKE</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="modele"
              id="puma"
              value="puma"
              v-model="filters.modele"
            />
            <label for="puma">Puma</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="modele"
              id="sx4"
              value="sx4"
              v-model="filters.modele"
            />
            <label for="sx4">Sx4 S-cross</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="modele"
              id="megane"
              value="megane"
              v-model="filters.modele"
            />
            <label for="megane">Mégane</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="modele"
              id="scenic"
              value="scenic"
              v-model="filters.modele"
            />
            <label for="scenic">Scénic</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="modele"
              id="trafic"
              value="trafic"
              v-model="filters.modele"
            />
            <label for="trafic">Trafic</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="modele"
              id="clio"
              value="clio"
              v-model="filters.modele"
            />
            <label for="clio">Clio</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="modele"
              id="captur"
              value="captur"
              v-model="filters.modele"
            />
            <label for="captur">Captur</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="modele"
              id="kadjar"
              value="kadjar"
              v-model="filters.modele"
            />
            <label for="kadjar">Kadjar</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="modele"
              id="koleos"
              value="koleos"
              v-model="filters.modele"
            />
            <label for="koleos">Koleos</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="modele"
              id="megane"
              value="megane"
              v-model="filters.modele"
            />
            <label for="megane">Mégane</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="modele"
              id="scenic"
              value="scenic"
              v-model="filters.modele"
            />
            <label for="scenic">Scénic</label>
          </div>
        </div>

        <div class="filter-section filter-section-collapse">
          <button class="collapse-btn flex justify-between w-full">
            <h3 class="title">Kilometrage</h3>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              class="w-6 h-6"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M19.5 8.25l-7.5 7.5-7.5-7.5"
              />
            </svg>
          </button>

          <!-- group of radio buttons ( 0 - 10000, 10000 - 20000, 40000 - 60000, 100000 - 150000, 150000 - 200000 ) -->
          <div class="filter-item">
            <input
              type="radio"
              name="kilometrage"
              id="toutes-kilometrage"
              value="toutes"
              v-model="filters.kilometrage"
            />
            <label for="toutes-kilometrage">Toutes</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="kilometrage"
              id="0-10000"
              value="0-10000"
              v-model="filters.kilometrage"
            />
            <label for="0-10000">0 - 10000</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="kilometrage"
              id="10000-20000"
              value="10000-20000"
              v-model="filters.kilometrage"
            />
            <label for="10000-20000">10000 - 20000</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="kilometrage"
              id="40000-60000"
              value="40000-60000"
              v-model="filters.kilometrage"
            />
            <label for="40000-60000">40000 - 60000</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="kilometrage"
              id="100000-150000"
              value="100000-150000"
              v-model="filters.kilometrage"
            />
            <label for="100000-150000">100000 - 150000</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="kilometrage"
              id="150000-200000"
              value="150000-200000"
              v-model="filters.kilometrage"
            />
            <label for="150000-200000">150000 - 200000</label>
          </div>
        </div>

        <div class="filter-section filter-section-collapse">
          <button class="collapse-btn flex justify-between w-full">
            <h3 class="title">Annee</h3>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              class="w-6 h-6"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M19.5 8.25l-7.5 7.5-7.5-7.5"
              />
            </svg>
          </button>

          <!-- group of radio buttons ( 2010 - 2015, 2015 - 2020, 2020 - 2025 ) -->
          <div class="filter-item">
            <input
              type="radio"
              name="annee"
              id="toutes-annee"
              value="toutes"
              v-model="filters.annee"
            />
            <label for="toutes-annee">Toutes</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="annee"
              id="2005-2010"
              value="2005-2010"
              v-model="filters.annee"
            />
            <label for="2005-2010">2005 - 2010</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="annee"
              id="2010-2015"
              value="2010-2015"
              v-model="filters.annee"
            />
            <label for="2010-2015">2010 - 2015</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="annee"
              id="2015-2020"
              value="2015-2020"
              v-model="filters.annee"
            />
            <label for="2015-2020">2015 - 2020</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="annee"
              id="2020-2025"
              value="2020-2025"
              v-model="filters.annee"
            />
            <label for="2020-2025">2020 - 2025</label>
          </div>
        </div>

        <div class="filter-section filter-section-collapse">
          <button class="collapse-btn flex justify-between w-full">
            <h3 class="title">Couleur</h3>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              class="w-6 h-6"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M19.5 8.25l-7.5 7.5-7.5-7.5"
              />
            </svg>
          </button>

          <!-- group of radio buttons ( blanc, noir, gris, bleu, rouge, vert ) -->
          <div class="filter-item">
            <input
              type="radio"
              name="couleur"
              id="toutes-couleur"
              value="toutes"
              v-model="filters.couleur"
            />
            <label for="toutes-couleur">Toutes</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="couleur"
              id="blanc"
              value="blanc"
              v-model="filters.couleur"
            />
            <label for="blanc">Blanc</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="couleur"
              id="noir"
              value="noir"
              v-model="filters.couleur"
            />
            <label for="noir">Noir</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="couleur"
              id="gris"
              value="gris"
              v-model="filters.couleur"
            />
            <label for="gris">Gris</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="couleur"
              id="bleu"
              value="bleu"
              v-model="filters.couleur"
            />
            <label for="bleu">Bleu</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="couleur"
              id="rouge"
              value="rouge"
              v-model="filters.couleur"
            />
            <label for="rouge">Rouge</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="couleur"
              id="vert"
              value="vert"
              v-model="filters.couleur"
            />
            <label for="vert">Vert</label>
          </div>
        </div>

        <div class="filter-section filter-section-collapse">
          <button class="collapse-btn flex justify-between w-full">
            <h3 class="title">Motorisation</h3>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              class="w-6 h-6"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M19.5 8.25l-7.5 7.5-7.5-7.5"
              />
            </svg>
          </button>

          <!-- group of radio buttons ( essence, diesel, electrique, hybred ) -->

          <div class="filter-item">
            <input
              type="radio"
              name="motorisation"
              id="toutes-motorisation"
              value="toutes"
              v-model="filters.motorisation"
            />
            <label for="toutes-motorisation">Toutes</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="motorisation"
              id="essence"
              value="essence"
              v-model="filters.motorisation"
            />
            <label for="essence">Essence</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="motorisation"
              id="diesel"
              value="diesel"
              v-model="filters.motorisation"
            />
            <label for="diesel">Diesel</label>
          </div>
          <div class="filter-item">
            <input
              type="radio"
              name="motorisation"
              id="electrique"
              value="electrique"
              v-model="filters.motorisation"
            />
            <label for="electrique">Electrique</label>
          </div>
        </div>

        <div class="filter-section filter-section-collapse">
          <button class="collapse-btn flex justify-between w-full">
            <h3 class="title">Equipement</h3>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              class="w-6 h-6"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M19.5 8.25l-7.5 7.5-7.5-7.5"
              />
            </svg>
          </button>

          <!-- group of checkbox ( climatisation, gps, camera, bluetooth, toit ouvrant, sieges chauffants, sieges en cuir, sieges electriques ) -->

          <div class="filter-item">
            <input
              type="checkbox"
              name="equipement"
              id="climatisation"
              value="climatisation"
              v-model="filters.equipement"
            />
            <label for="climatisation">Climatisation</label>
          </div>
          <div class="filter-item">
            <input
              type="checkbox"
              name="equipement"
              id="gps"
              value="gps"
              v-model="filters.equipement"
            />
            <label for="gps">GPS</label>
          </div>
          <div class="filter-item">
            <input
              type="checkbox"
              name="equipement"
              id="camera"
              value="camera"
              v-model="filters.equipement"
            />
            <label for="camera">Camera</label>
          </div>
          <div class="filter-item">
            <input
              type="checkbox"
              name="equipement"
              id="bluetooth"
              value="bluetooth"
              v-model="filters.equipement"
            />
            <label for="bluetooth">Bluetooth</label>
          </div>
          <div class="filter-item">
            <input
              type="checkbox"
              name="equipement"
              id="toit-ouvrant"
              value="toit-ouvrant"
              v-model="filters.equipement"
            />
            <label for="toit-ouvrant">Toit ouvrant</label>
          </div>
          <div class="filter-item">
            <input
              type="checkbox"
              name="equipement"
              id="sieges-chauffants"
              value="sieges-chauffants"
              v-model="filters.equipement"
            />
            <label for="sieges-chauffants">Sieges chauffants</label>
          </div>
          <div class="filter-item">
            <input
              type="checkbox"
              name="equipement"
              id="sieges-en-cuir"
              value="sieges-en-cuir"
              v-model="filters.equipement"
            />
            <label for="sieges-en-cuir">Sieges en cuir</label>
          </div>
          <div class="filter-item">
            <input
              type="checkbox"
              name="equipement"
              id="sieges-electriques"
              value="sieges-electriques"
              v-model="filters.equipement"
            />
            <label for="sieges-electriques">Sieges electriques</label>
          </div>
        </div>
      </div>
    </div>

    <div class="app-content">
      <div class="app-header">
        <label for="">
          <span class="nb-items">{{ pagination.count }} resultats</span>
          correspondant a votre recherche
        </label>
        <div class="flex ml-auto sort-by">
          <label for="">Trier par</label>
          <select name="" id="" v-model="filters.sort">
            <option value="">Default</option>
            <option value="price asc">Prix croissant</option>
            <option value="price desc">Prix decroissant</option>
            <option value="year asc">Annee croissant</option>
            <option value="year desc">Annee decroissant</option>
            <option value="brand asc">Marque croissant</option>
            <option value="brand desc">Marque decroissant</option>
            <option value="model asc">Modele croissant</option>
            <option value="model desc">Modele decroissant</option>
          </select>
        </div>
      </div>

      <div class="app-body">
        <div class="grid lg:grid-cols-3 md:grid-cols-2 grid-cols-1 gap-3">
          <!-- fale 3 loading items using tailwind loading styles -->
          <template v-if="loading">
            <div class="item" v-for="n in 12" :key="n">
              <div class="media">
                <div class="w-full h-48 bg-gray-100 animate-pulse"></div>
              </div>
              <div class="item-body">
                <div class="flex justify-between w-full">
                  <div class="left flex flex-col flex-1 p-2">
                    <div
                      class="w-full mt-2 h-4 bg-gray-300 animate-pulse rounded"
                    ></div>
                    <div
                      class="w-full mt-2 h-4 bg-gray-300 animate-pulse rounded"
                    ></div>
                    <div
                      class="w-full mt-2 h-4 bg-gray-300 animate-pulse rounded"
                    ></div>
                  </div>
                  <div class="right flex flex-col flex-1 items-end p-2 rounded">
                    <div
                      class="w-full mt-2 h-6 bg-gray-300 animate-pulse rounded"
                    ></div>
                    <div
                      class="w-full mt-2 h-4 bg-gray-300 animate-pulse rounded"
                    ></div>
                    <div
                      class="w-full mt-2 h-4 bg-gray-300 animate-pulse rounded"
                    ></div>
                  </div>
                </div>
              </div>
            </div>
          </template>
          <template v-else>
            <template v-for="(v, i) in vehicles">
              <div v-if="i == 4" class="aditem" :key="'ad' + v.id">
                <div class="bg"></div>
                <div class="content">
                  <div class="text">
                    Vous ne trouves pas votre bonheur ? Nous faisons la
                    recherche pour vous
                  </div>
                  <button>
                    <svg
                      xmlns="http://www.w3.org/2000/svg"
                      fill="none"
                      viewBox="0 0 24 24"
                      stroke-width="1.5"
                      stroke="currentColor"
                      class="w-6 h-6"
                    >
                      <path
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        d="M17.25 8.25L21 12m0 0l-3.75 3.75M21 12H3"
                      />
                    </svg>

                    Découvrir
                  </button>
                </div>
              </div>

              <div :key="v.id">
                <div class="item">
                  <div class="media">
                    <template v-if="v.pics.length">
                      <img :src="v.pics[0]" alt="" />
                    </template>
                    <template v-else>
                      <img
                        src="http://localhost:8000/generic-sedan-silo.jpg"
                        alt=""
                      />
                    </template>
                  </div>
                  <div class="item-body">
                    <div class="flex justify-between w-full">
                      <div class="left flex flex-col">
                        <div class="brand">{{ v.brand }}</div>
                        <div class="model">{{ v.model }}</div>
                        <div class="version">{{ v.version }}</div>
                        <div class="more">
                          {{
                            v.year + " - " + v.energy + " - " + v.power + "ch"
                          }}
                        </div>
                      </div>
                      <div class="right flex flex-col place-items-end">
                        <div class="price">{{ v.price | priceFilter }}</div>
                        <div class="price-retail" v-if="v.priceRetail != null">
                          <div class="price-retail-value">
                            {{ v.priceRetail | priceFilter }}
                          </div>
                          <div class="price-diff">
                            {{
                              getProceDiffPercentage(v.priceRetail, v.price)
                            }}%
                          </div>
                        </div>
                        <div class="price-monthly" v-if="v.priceMonthly">
                          ou à partir de <br />
                          <span class="price-monthly-value">{{
                            v.priceMonthly | priceFilter
                          }}</span>
                          <br />
                          /mois
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </template>
          </template>
        </div>
        <!-- pagination in center -->
        <div class="pagination flex justify-center">
          <div class="pagination-item" @click="prev()">
            <button>Prev</button>
          </div>
          <div
            class="pagination-item"
            :class="{ current: pagination.page == n }"
            v-for="n in pagination.pages"
            :key="n"
            @click="loadVehicles(n)"
          >
            <button>{{ n }}</button>
          </div>
          <div class="pagination-item" @click="next()">
            <button>Next</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import BetweenInput from "../components/reusable/BetweenInput.vue";
import ToggleInput from "../components/reusable/ToggleInput.vue";
import ChoicesInput from "../components/reusable/ChoicesInput.vue";
import axios from "axios";

export default {
  name: "IndexPage",
  components: {
    BetweenInput,
    ToggleInput,
    ChoicesInput,
  },
  data() {
    return {
      filters: {
        pretAPartir: true,
        zeroKm: true,
        promotions: false,
        budgetType: "Total",
        between: [1000, 100000],
        betweenMax: 100000,
        betweenMin: 1000,
        marque: "toutes",
        type: "toutes",
        modele: "toutes",
        kilometrage: "toutes",
        annee: "toutes",
        couleur: "toutes",
        motorisation: "toutes",
        equipement: "toutes",
        sort: "",
      },
      vehicles: [],
      pagination: {
        count: 0,
        page: 0,
        limit: 0,
        pages: 0,
        offset: 0,
      },
      loading: false,
      last_time_filter: 0,
    };
  },
  filters: {
    priceFilter(value) {
      if (value == null) return "Prix non communiqué";
      // price filter without coma
      return value.toString().replace(/\B(?=(\d{3})+(?!\d))/g, " ") + " €";
    },
  },
  computed: {
    // filters.budgetType
    budgetType() {
      return this.filters.budgetType;
    },
    betweenMin() {
      return this.filters.between[0];
    },
    betweenMax() {
      return this.filters.between[1];
    },
  },
  watch: {
    filters: {
      // old and new
      handler(newVal, oldVal) {
        if (this.last_time_filter + 1000 > Date.now()) {
          return;
        }

        this.last_time_filter = Date.now();

        this.loadVehicles();
      },
      deep: true,
    },
    budgetType() {
      if (this.budgetType == "Mensuel") {
        this.filters.betweenMax = 2500;
        this.filters.betweenMin = 100;
        this.filters.between = [100, 2500];
        return;
      }

      this.filters.betweenMax = 100000;
      this.filters.betweenMin = 1000;
      this.filters.between = [1000, 100000];
    },
    betweenMin() {
      this.loadVehicles();
    },
    betweenMax() {
      this.loadVehicles();
    },
  },
  mounted() {
    this.initCollapse();

    this.loadVehicles();
  },
  methods: {
    loadVehicles(page = 1) {
      if (page < 1) {
        return;
      }

      if (this.pagination.pages != 0)
        if (page > this.pagination.pages) {
          return;
        }

      this.loading = true;

      axios
        .get(`http://localhost:8000/vehicles/filter`, {
          params: {
            page: page,
            limit: 12,
            pretAPartir: this.filters.pretAPartir ?? null,
            zeroKm: this.filters.zeroKm ?? null,
            promotions: this.filters.promotions ?? null,
            budgetType: this.filters.budgetType ?? null,
            between: this.filters.between ?? null,
            marque:
              this.filters.marque == "toutes" ? null : this.filters.marque,
            type: this.filters.type == "toutes" ? null : this.filters.type,
            modele:
              this.filters.modele == "toutes" ? null : this.filters.modele,
            kilometrage:
              this.filters.kilometrage == "toutes"
                ? null
                : this.filters.kilometrage,
            annee: this.filters.annee == "toutes" ? null : this.filters.annee,
            couleur:
              this.filters.couleur == "toutes" ? null : this.filters.couleur,
            motorisation:
              this.filters.motorisation == "toutes"
                ? null
                : this.filters.motorisation,
            equipement:
              this.filters.equipement == "toutes"
                ? null
                : this.filters.equipement,
            sort: this.filters.sort ? this.filters.sort : null,
          },
          headers: {
            "Content-Type": "application/json",
            Accept: "application/json",
          },
        })
        .then((response) => {
          console.log(response.data);
          let data = response.data.data;
          this.vehicles = data.data;
          this.pagination.page = data.page;
          this.pagination.limit = data.limit;
          this.pagination.pages = data.pages;
          this.pagination.offset = data.offset;
          this.pagination.count = data.count;

          this.loading = false;
        })
        .catch((error) => {
          console.log(error);
          this.loading = false;
        });
    },
    initCollapse() {
      // get all filter-section-collapse except who contains .active class
      const filterSectionCollapse = document.querySelectorAll(
        ".filter-section-collapse"
      );

      // collapse filter section
      const collapseFilterSection = (filterSection, i) => {
        let activeHeight = 0;
        // get elem attribute data-height
        activeHeight += parseInt(filterSection.getAttribute("data-height"));
        // get the padding-top & padding-bottom of the filter-section
        activeHeight += parseInt(
          window.getComputedStyle(filterSection).paddingTop
        );
        activeHeight += parseInt(
          window.getComputedStyle(filterSection).paddingBottom
        );

        // get the height of the .collapse-btn
        let collapseHeight =
          filterSection.querySelector(".collapse-btn").offsetHeight;
        collapseHeight += parseInt(
          window.getComputedStyle(filterSection).paddingTop
        );
        collapseHeight += parseInt(
          window.getComputedStyle(filterSection).paddingBottom
        );

        // check if contain .active class
        if (filterSection.classList.contains("active")) {
          filterSection.style.height = `${activeHeight}px`;
        } else {
          filterSection.style.height = `${collapseHeight}px`;
        }
      };

      // add event listener to each filter-section-collapse
      filterSectionCollapse.forEach((filterSection) => {
        let collapseBtn = filterSection.querySelector(".collapse-btn");

        // get filterSection height
        let filterSectionHeight = filterSection.offsetHeight;

        // set data-height attribute to the filter-section
        filterSection.setAttribute("data-height", filterSectionHeight);

        collapseFilterSection(filterSection);

        // add click event listener to .collapse-btn
        collapseBtn.addEventListener("click", () => {
          // if the filter-section contains .active class
          if (filterSection.classList.contains("active")) {
            // remove .active class
            filterSection.classList.remove("active");
          } else {
            // add .active class
            filterSection.classList.add("active");
          }

          collapseFilterSection(filterSection);
        });
      });
    },
    getProceDiffPercentage(priceRetail, price) {
      if (!priceRetail || !price) return 0;
      if (priceRetail == 0) return 0;
      return Math.round(((price - priceRetail) / priceRetail) * 100);
    },
    next() {
      this.loadVehicles(parseInt(this.pagination.page) + 1);
    },
    prev() {
      this.loadVehicles(parseInt(this.pagination.page) - 1);
    },
    showSideBar() {
      // add .show to .app-side-bar
      let sb = document.querySelector(".app-side-bar");
      if (sb.classList.contains("show")) {
        sb.classList.remove("show");
      } else {
        sb.classList.add("show");
      }
    },
    hideSideBar() {
      // add .show to .app-side-bar
      let sb = document.querySelector(".app-side-bar");
      if (sb.classList.contains("show")) {
        sb.classList.remove("show");
      } else {
        sb.classList.add("show");
      }
    },
  },
};
</script>

<style scoped>
.app-side-bar * {
  font-family: Druk, sans-serif;
}
.app-side-bar-container > .title {
  font-weight: 800;
  font-size: 18px;
  text-transform: uppercase;
  color: #042a38;
  font-style: normal;
  letter-spacing: -1px;
  transform: scale(1, 2);
  margin-bottom: 30px;
}

.app-side-bar {
  min-width: 300px;
  padding: 20px;
  height: 100%;
  overflow-y: scroll;
}

/* light scrollbar */
.app-side-bar::-webkit-scrollbar {
  width: 5px;
}

.app-side-bar .filter-section {
  padding: 10px 0;
  border-top: 1px solid #e5e5e5;
}

.filter-section-collapse {
  overflow: hidden;
  transition: all 0.2s ease-in-out;
}

.filter-section-collapse > * {
  opacity: 0;
}
.filter-section-collapse > *:first-child {
  opacity: 1;
}

.filter-section-collapse.active > * {
  opacity: 1;
}

.filter-section-collapse svg {
  width: 20px;
  transition: all 0.2s ease-in-out;
}

.filter-section-collapse.active svg {
  transform: rotate(180deg);
}

.app-side-bar .filter-section .title {
  font-size: 15px;
  font-weight: bold;
  margin-bottom: 10px;
  color: #042a38;
}

.app-side-bar .filter-section .filter-item {
  display: flex;
  align-items: center;
  margin-bottom: 5px;
  width: 100%;
}

.app-side-bar .filter-section.toggles .filter-item {
  background: #18495c;
  color: white;
  padding: 8px 14px;
  border-radius: 5px;
  opacity: 0.5;
  transition: all 0.2s ease-in-out;
}

.app-side-bar .filter-section.toggles .filter-item.active {
  opacity: 1;
}

.app-side-bar .filter-section .filter-item input {
  margin-right: 5px;
}

.app-side-bar .filter-section .filter-item label {
  font-size: 14px;
  font-weight: 500;
  margin-left: 8px;
  width: 100%;
}

.app-content {
  display: flex;
  flex-direction: column;
  width: 100%;
}

.app-content {
  display: flex;
  flex-direction: column;
  width: 100%;
  padding: 20px;
}

.app-content .app-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 18px;
  width: 100%;
}

.app-content .app-header .title {
  font-size: 20px;
  font-weight: bold;
  color: #042a38;
}

.app-content .app-header label {
  font-size: 14px;
  color: #042a38;
}
.app-content .app-header .nb-items {
  font-weight: bold;
}

.app-content .app-header .sort-by {
  display: flex;
  align-items: center;
}

.app-content .app-header .sort-by label {
  margin-right: 10px;
}

.app-content .app-header .sort-by select {
  padding: 3px 10px;
  border-radius: 5px;
  font-size: 14px;
  color: #042a38;
  background: #ecf1f2;
}

.item {
  display: flex;
  flex-direction: column;
  width: 100%;
  border-radius: 5px;
  background: #ecf1f2;
  margin-bottom: 10px;
  border: 1px solid #e5e5e5;
  transition: all 0.2s ease-in-out;
}

.item .media {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}

.item .media img {
  width: 100%;
  min-height: 200px;
  height: 200px;
  object-fit: cover;
}

.item .item-body {
  display: flex;
  justify-content: space-between;
  width: 100%;
  padding: 10px;
  height: 140px;
  background-color: #eff8f9;
}

.item .item-body .brand {
  font-weight: 500;
  color: #50b6c4;
  /* uppercase */
  text-transform: uppercase;
}

.item .item-body .model {
  /* like title */
  font-weight: 800;
  font-size: 15px;
  text-transform: uppercase;
  color: #042a38;
  font-style: normal;
  letter-spacing: -1px;
  transform: scale(1, 2);
  margin-bottom: 7px;
  margin-top: 7px;
}

.item .item-body .version {
  font-weight: 500;
  font-size: 14px;
  color: #042a38;
}

.item .item-body .more {
  font-size: 14px;
  color: #042a38;
}

.item .item-body .price {
  font-weight: 700;
  font-size: 22px;
  color: #042a38;
  white-space: nowrap;
}

.item .item-body .price-retail {
  font-weight: 700;
  font-size: 12px;
  color: #042a38;
  display: flex;
  align-items: center;
}
.item .item-body .price-retail-value {
  text-decoration: line-through;
  color: #042a38;
}

.item .item-body .price-diff {
  color: #042a38;
  font-size: 11px;
  background: #ffa70e;
  border-radius: 3px;
  padding: 1 px 5px;
  margin-left: 5px;
}

.item .item-body .price-monthly {
  font-size: 12px;
  color: #597d87;
  margin-top: 5px;
  /* space between lines */
  line-height: 1;
  text-align: right;
  margin-top: 10px;
}

.item .item-body .price-monthly .price-monthly-value {
  font-weight: 700;
  font-size: 15px;
}

.item:hover {
  box-shadow: 0 0 10px 0 rgba(0, 0, 0, 0.052);
  cursor: pointer;
  transform: scale(1.01);
}

/* <div v-if="i == 4" class="aditem" :key="'ad'+v.id">
                  <div class="bg"></div>
                  <div class="content">
                    <div class="text">
                      Vous ne trouves pas votre bonheur ? Nous faisons la recherche pour vous
                    </div>
                    <button>Découvrir</button>
                  </div>
              </div> */

.aditem {
  display: flex;
  flex-direction: column;
  width: 100%;
  border-radius: 5px;
  background: #ecf1f2;
  margin-bottom: 10px;
  border: 1px solid #e5e5e5;
  transition: all 0.2s ease-in-out;
  background: url("http://localhost:8000/Nouveau-Dacia-Duster.jpg");
  background-size: cover;
  background-position: center;
  position: relative;
}

.aditem .bg {
  /* gradian background to the bottom of screen */
  background: linear-gradient(
    180deg,
    rgba(0, 0, 0, 0) 20%,
    /* rgba(0, 0, 0, 0.8) 70%, */ rgb(0, 0, 0) 100%
  );
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 0;
}

.aditem .content {
  display: flex;
  flex-direction: column;
  justify-content: end;
  align-items: center;
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 1;
  padding: 30px 0;
  transition: all 0.2s ease-in-out;
}

.aditem .content .text {
  color: white;
  font-size: 20px;
  text-align: center;
  margin-bottom: 20px;
  padding: 0 20px;
}

.aditem .content button {
  padding: 10px 20px;
  border-radius: 5px;
  background: transparent;
  border: 1px solid white;
  color: white;
  font-size: 14px;
  cursor: pointer;
  border-radius: 20px;
  display: flex;
  items-align: center;
}

.aditem .content button svg {
  margin-right: 8px;
  transition: all 0.2s ease-in-out;
}

.aditem .content button:hover svg {
  transform: translateX(5px);
}

.aditem:hover {
  box-shadow: 0 0 10px 0 rgba(0, 0, 0, 0.052);
  cursor: pointer;
  transform: scale(1.01);
}

.aditem:hover .bg {
  background: linear-gradient(180deg, rgba(0, 0, 0, 0) 10%, rgb(0, 0, 0) 100%);
}
.aditem:hover .content {
  padding-bottom: 40px;
}

.pagination {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 20px;
}

.pagination .pagination-item {
  display: flex;
  justify-content: center;
  align-items: center;
  min-width: 30px;
  border-radius: 5px;
  background: #eff8f9;
  margin-right: 5px;
  cursor: pointer;
  padding: 3px 8px;
  font-size: 14px;
}

.pagination .pagination-item.current {
  background: #042a38;
  color: white;
}

.show-button {
  display: none;
}

.hide-button {
  display: none;
}

/* if screen less than 1280px */
@media (max-width: 1280px) {
  .app-side-bar {
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    scroll-behavior: smooth;
    overflow: hidden;
    z-index: 101;
    overflow-y: scroll;
    background: white;
    transform: translateX(-100%);
    transition: all 0.2s ease-in-out;
  }

  .app-side-bar.show {
    transform: translateX(0);
  }

  .show-button {
    display: flex;
    position: fixed;
    padding: 12px;
    left: 0;
    top: 0;
    color: white;
    font-weight: 700;
    background: #042a38;
    border: 1px solid #042a3840;
    border-top: 0px;
    border-left: 0;
    border-end-end-radius: 5px;
    box-shadow: 1px 1px 5px #0000003b;
    z-index: 100;
    align-items: center;
  }

  .show-button svg {
    width: 14px;
    margin-right: 5px;
    /* change svg color */
    fill: white;
    color:white;
  }

  .hide-button {
    display: flex;
    position: absolute;
    padding: 4px 8px;
    right: 0;
    top: 0;
    color: red;
    font-size: 28px;
  }
}
</style>
