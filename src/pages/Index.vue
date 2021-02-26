<template>
  <q-page class="flex flex-center">
    <q-stepper
      v-model="step"
      ref="stepper"
      color="primary"
      animated
      alternative-labels
    >

    <!---------------------------------------------------->
    <!---------------------- PART 1 ---------------------->
    <!---------------------------------------------------->
      <q-step
        prefix="1"
        :name="1"
        title="Données Personnelles"
        icon="settings"
        :done="done1"
        :error="stateForm1"
      >
        <q-form ref="myForm1">
          <div class="row form">
            <div class="col-md-6 col-sm-6 col-xs-12 innerColumn">
              <p>Type d'Inscription</p>
              <q-select v-model="P1TypeInscription" :options="typeInscription" label="inscription" />
            </div>
            <div class="col-md-6 col-sm-6 col-xs-12 innerColumn">
              <p>Date d'Enregistrement</p>	
              <div>
                <q-input v-model="P1DateInscription" type="date" />
              </div>
            </div>
          </div>

          <div class="row form">
            <div class="col-md-6 col-sm-6 col-xs-12 innerColumn">
              <p>Nom de Famille</p>
              <q-input
                type="text"
                v-model="P1NomDeFamille"
                autogrow
                label="Nom de Famille"
              />
            </div>
            <div class="col-md-6 col-sm-6 col-xs-12 innerColumn">
              <p>Prénom</p>
              <q-input
                type="text"
                v-model="P1Prenom"
                autogrow
                label="Prénom"
              />
            </div>
          </div>

          <div class="row form">
            <div class="col-md-6 col-sm-6 col-xs-12 innerColumn">
              <p>Date de Naissance</p>
              <div>
                <q-input v-model="P1BirthDate" type="date" />
              </div>
            </div>
            <div class="col-md-6 col-sm-6 col-xs-12 innerColumn">
              <p>Sexe</p>
              <q-select v-model="P1Sexe" :options="Sexe" label="Sexe" />
            </div>
          </div>
          
          <div class="row form">
            <div class="col-md-6 col-sm-6 col-xs-12 innerColumn">
              <p>Lieu de Naissance</p>
              <q-input
                type="text"
                v-model="P1LieuDeNaissance"
                autogrow
                label="Lieu de Naissance"
              />
            </div>
            <div class="col-md-6 col-sm-6 col-xs-12 innerColumn">
              <p>Adresse Email</p>
              <q-input
                type="email"
                v-model="P1Email"
                autogrow
                label="Adresse Email"
              />
            </div>
          </div>

          <div class="row form">
            <div class="col-md-6 col-sm-6 col-xs-12 innerColumn">
              <p>Numéro de Téléphone</p>
              <q-input
                type="tel"
                v-model="P1Telephone"
                mask="########"
                hint="Numéro Béninois, sans espaces"
                autogrow
                label="Numéro de Téléphone"
              />
            </div>
            <div class="col-md-6 col-sm-6 col-xs-12 innerColumn">
              <p>Adresse de Résidence</p>
              <q-input
                type="text"
                v-model="P1Adresse"
                autogrow
                label="Adresse de Résidence"
              />
            </div>
          </div>
          <div class="row form">
            <div class="col-md-6 col-sm-6 col-xs-12 innerColumn">
              <p>Classe d'Enregistrement</p>
              <q-select v-model="P1ClasseEnregistrement" :options="ClasseEnregistrement" label="Classe d'Enregistrement" />
            </div>
            <div class="col-md-6 col-sm-6 col-xs-12 innerColumn">
              <p></p>
            </div>
          </div>
        </q-form>
        <q-stepper-navigation style="float: right;">
          <q-btn @click="checkForm1()" icon-right="navigate_next" color="primary" label="Continue"></q-btn>
        </q-stepper-navigation>

      </q-step>


    <!---------------------------------------------------->
    <!---------------------- PART 2 ---------------------->
    <!---------------------------------------------------->
      <q-step
        prefix="2"
        :name="2"
        title="Informations Détaillées"
        icon="create_new_folder"
        :error="stateForm2"
        :done="done2"
      >
        <q-form ref="myForm2">
         <div class="row form">
            <div class="col-md-6 col-sm-6 col-xs-12 innerColumn">
              <p>Type de Notification</p>
              <q-select v-model="P2TypeNotification" :options="TypeNotification" label="Type de Notification" />
            </div>
            <div class="col-md-6 col-sm-6 col-xs-12 innerColumn">
              <p>Activité Extra-scolaire</p>
              <q-select v-model="P2ActiviteExtraScolaire" multiple :options="ActiviteExtraScolaire" label="Activité Extra-Scolaire" />
            </div>
          </div>

         <div class="row form">
            <q-btn 
              rounded
              color="white"
              style="background-color: teal; margin: 1rem auto 1rem auto;"
              flat
              icon="person"
              label="Ajouter un contact"
              @click="populateContact()"
            />
          </div>

          <hr />

         <div style="margin-bottom: 1rem;" class="row form">
          <q-table
            style="width: 100%;"
            :data="P2ContactData"
            :columns="P2ContactColumns"
            row-key="name"
          />
          </div>

          <hr />

          <p style="text-align: center;">Information Sanitaire</p>

          <div class="row form">
            <div class="col-md-6 col-sm-6 col-xs-12 innerColumn">
              <p>Groupe Sanguin</p>
              <q-select v-model="P2GroupeSanguin" :options="GroupeSanguin" label="Groupe Sanguin" />
            </div>
            <div class="col-md-6 col-sm-6 col-xs-12 innerColumn">
              <p>Maladie(s) Fréquente(s)</p>
              <q-input
                type="text"
                v-model="P2MaladieFrequente"
                autogrow
                label="Maladie(s) Fréquente(s)"
              />
            </div>
          </div>
        </q-form>

        <q-stepper-navigation style="float: right;">
          <q-btn unelevated  flat @click="step = 1" style="background-color: #D3D3D3" text-color="grey-9" icon="navigate_before" label="Previous" class="q-ml-sm" />
          <q-btn unelevated  @click="() => { done2 = true; step = 3 }" icon-right="navigate_next" color="primary" label="Continue" />
        </q-stepper-navigation>
      </q-step>


    <!---------------------------------------------------->
    <!---------------------- PART 3 ---------------------->
    <!---------------------------------------------------->
      <q-step
        prefix="3"
        :done="done3"
        :name="3"
        title="Paiement & Dossier d'inscription"
        icon="assignment"
        :error="stateForm3"
      >
        <q-form ref="myForm3">
          
          <div class="row form">
            <div class="col-md-6 col-sm-6 col-xs-12 innerColumn">
              <p>Type de Paiement</p>
              <q-select v-model="P3TypePaiement" :options="TypePaiement" label="Type de Paiement" />
            </div>
            <div class="col-md-6 col-sm-6 col-xs-12 innerColumn" style="display: flex; flex-direction: column; align-items: center">
              <p>Votre enfant peut-il pratiquer du sport ?</p>
              <q-radio v-model="P3DispenseSport" val="Non" label="Non" color="red" />
              <q-radio v-model="P3DispenseSport" val="Oui" label="Oui" color="green" />
            </div>
          </div>

          <div class="row form">
            <div class="col-md-6 col-sm-6 col-xs-12 innerColumn">
              <p>Modalité de Paiement</p>
              <q-select v-model="P3ModalitePaiement" :options="ModalitePaiement" label="Modalité de Paiement" />
            </div>
            
          </div>

          <div class="row form">
            <div class="col-md-6 col-sm-6 col-xs-12 innerColumn">
              <p>Décrivez votre enfant en quelques lignes</p>
              <q-input 
                v-model="P3Description"
                type="textarea"
              />
            </div>
            <div class="col-md-6 col-sm-6 col-xs-12 innerColumn" style="display: flex; flex-direction: column; align-items: center">
              <p>Bulletin de note de la classe précédente</p>
              <q-uploader
                style="max-width: 1000px"
                url="http://localhost:4444/upload"
                multiple
                label="PDF ou DOC (Max 2Mb)"
                :filter="checkFile"
                @rejected="onRejected">
                <template v-slot:list="scope">
                  <p style="text-align: center; color: #D1D1D1;">Glissez et déposez vos fichiers ici</p>
                  <q-list separator>

                    <q-item v-for="file in scope.files" :key="file.name">
                      <q-item-section>
                        <q-item-label class="full-width ellipsis">
                          {{ file.name }}
                        </q-item-label>

                        <q-item-label caption>
                          Status: {{ file.__status }}
                        </q-item-label>

                        <q-item-label caption>
                          {{ file.__sizeLabel }} / {{ file.__progressLabel }}
                        </q-item-label>
                      </q-item-section>

                      <q-item-section
                        v-if="file.__img"
                        thumbnail
                        class="gt-xs"
                      >
                        <img :src="file.__img.src">
                      </q-item-section>

                      <q-item-section top side>
                        <q-btn
                          class="gt-xs"
                          size="12px"
                          flat
                          dense
                          round
                          icon="delete"
                          @click="scope.removeFile(file)"
                        />
                      </q-item-section>
                    </q-item>

                  </q-list>
                </template>
              </q-uploader>
            </div>
          </div>
          
        </q-form>

        <q-stepper-navigation style="float: right;">
          <q-btn flat @click="step = 2" style="background-color: #D3D3D3" text-color="grey-9" label="Previous" class="q-ml-sm" icon="navigate_before"></q-btn>
          <q-btn @click="() => { done3 = true; step = 4 }" color="primary" icon-right="navigate_next" label="Continue"></q-btn>
        </q-stepper-navigation>
      </q-step>


    <!---------------------------------------------------->
    <!---------------------- PART 4 ---------------------->
    <!---------------------------------------------------->
      <q-step
        prefix="4"
        :name="4"
        :done="done4"
        title="Informations Supplémentaires"
        icon="add_comment"
        :error="stateForm4"
      >

        <q-form ref="myForm4">

          <div class="row form">
              <div class="col-md-6 col-sm-6 col-xs-12 innerColumn">
                <p>Demande Manuscrite</p>
                <q-uploader
                  style="max-width: 1000px"
                  url="http://localhost:4444/upload"
                  multiple
                  label="PDF ou DOC (Max 2Mb)"
                  :filter="checkFile"
                  @rejected="onRejected">
                  <template v-slot:list="scope">
                    <p style="text-align: center; color: #D1D1D1;">Glissez et déposez vos fichiers ici</p>
                    <q-list separator>

                      <q-item v-for="file in scope.files" :key="file.name">
                        <q-item-section>
                          <q-item-label class="full-width ellipsis">
                            {{ file.name }}
                          </q-item-label>

                          <q-item-label caption>
                            Status: {{ file.__status }}
                          </q-item-label>

                          <q-item-label caption>
                            {{ file.__sizeLabel }} / {{ file.__progressLabel }}
                          </q-item-label>
                        </q-item-section>

                        <q-item-section
                          v-if="file.__img"
                          thumbnail
                          class="gt-xs"
                        >
                          <img :src="file.__img.src">
                        </q-item-section>

                        <q-item-section top side>
                          <q-btn
                            class="gt-xs"
                            size="12px"
                            flat
                            dense
                            round
                            icon="delete"
                            @click="scope.removeFile(file)"
                          />
                        </q-item-section>
                      </q-item>

                    </q-list>
                  </template>
                </q-uploader> 
              </div>
              <div class="col-md-6 col-sm-6 col-xs-12 innerColumn">
                <p>Image d'affichage</p>
                <q-uploader
                  style="max-width: 1000px"
                  url="http://localhost:4444/upload"
                  multiple
                  label="PDF ou DOC (Max 2Mb)"
                  :filter="checkFile"
                  @rejected="onRejected">
                  <template v-slot:list="scope">
                    <p style="text-align: center; color: #D1D1D1;">Glissez et déposez vos fichiers ici</p>
                    <q-list separator>

                      <q-item v-for="file in scope.files" :key="file.name">
                        <q-item-section>
                          <q-item-label class="full-width ellipsis">
                            {{ file.name }}
                          </q-item-label>

                          <q-item-label caption>
                            Status: {{ file.__status }}
                          </q-item-label>

                          <q-item-label caption>
                            {{ file.__sizeLabel }} / {{ file.__progressLabel }}
                          </q-item-label>
                        </q-item-section>

                        <q-item-section
                          v-if="file.__img"
                          thumbnail
                          class="gt-xs"
                        >
                          <img :src="file.__img.src">
                        </q-item-section>

                        <q-item-section top side>
                          <q-btn
                            class="gt-xs"
                            size="12px"
                            flat
                            dense
                            round
                            icon="delete"
                            @click="scope.removeFile(file)"
                          />
                        </q-item-section>
                      </q-item>

                    </q-list>
                  </template>
                </q-uploader>
              </div>
            </div>

            <div class="row">
              <div class="col-md-12 col-sm-12 col-xs-12 innerColumn">
              <p>Observation</p>
              <q-input
                label="Si vous avez une information à ajouter, veuillez l'écrire ici" 
                v-model="P4Observation"
                type="textarea"
                style="max-width: 2000px"
              />
              </div>
            </div>

        </q-form>

        <q-stepper-navigation style="float: right;">
          <q-btn flat @click="step = 3"  style="background-color: #D3D3D3" text-color="grey-9" label="Previous" class="q-ml-sm" icon="navigate_before"></q-btn>
          <q-btn @click="() => { done4 = true; step = 5 }" color="primary" icon-right="navigate_next" label="Récapitulatif"></q-btn>
        </q-stepper-navigation>
      </q-step>

    <!---------------------------------------------------->
    <!---------------------- PART 5 ---------------------->
    <!---------------------------------------------------->
      <q-step
        prefix="5"
        :name="5"
        :done="done5"
        title="Récapitulatif"
        icon="paper"
        :error="stateForm5"
      >
      
        <div class="recap">
          <h2>Récapitulatif de l'inscription</h2>
          <div class="row">
            <div class="col-md-6 col-sm-6 col-xs-12 innerColumn">
              <hr />
              <h4>Données Personnelles</h4>
              
              <p>Type d'inscription : </p>
              <p>{{P1TypeInscription}}</p>

              <p>Date d'inscription : </p>
              <p>{{P1DateInscription}}</p>

              <p>Nom de Famille : </p>
              <p>{{P1NomDeFamille}}</p>

              <p>Prénom(s) : </p>
              <p>{{P1Prenom}}</p>

              <p>Date de Naissance : </p>
              <p>{{P1BirthDate}}</p>

              <p>Sexe : </p>
              <p>{{P1Sexe}}</p>

              <p>Lieu de Naissance : </p>
              <p>{{P1LieuDeNaissance}}</p>

              <p>Email : </p>
              <p>{{P1Email}}</p>

              <p>Téléphone : </p>
              <p>{{P1Telephone}}</p>

              <p>Adresse de Résidence : </p>
              <p>{{P1Adresse}}</p>

              <p>Classe d'Enregistrement : </p>
              <p>{{P1ClasseEnregistrement}}</p>
            </div>

            <div class="col-md-6 col-sm-6 col-xs-12 innerColumn">
              <hr />
              <h4>Informations Détaillées</h4>

              <p>Type de Notification : </p>
              <p>{{P2TypeNotification}}</p>
              
              <p>Activité(s) Extra-scolaire : </p>
              <p v-for="activity in P2ActiviteExtraScolaire" :key="activity">{{activity}}</p>

              <p>Contacts : </p>
              <p v-for='contact in P2ContactPerson' :key="contact.nom" >{{contact.nom}} {{contact.prenom}}</p>  

              <p>Groupe Sanguin : </p>
              <p>{{P2GroupeSanguin}}</p>

              <p>Maladie(s) Fréquentes : </p>
              <p>{{P2MaladieFrequente}}</p>

              <hr />
              <h4>Paiement & Dossier d'Inscription</h4>

              <p>Type de Paiement : </p>
              <p>{{P3TypePaiement}}</p>

              <p>Dispense de sport : </p>
              <p>{{P3DispenseSport}}</p>

              <p>Modalité de Paiement : </p>
              <p>{{P3ModalitePaiement}}</p>

              <p>Description de l'enfant : </p>
              <p>{{P3Description}}</p>

              <hr />
              <h4>Informations Supplémentaires</h4>
              <p>Observations : {{P4Observation}}</p>
            </div>
          </div>

        </div>

        <q-stepper-navigation style="float: right;">
          <q-btn flat @click="step = 4"  style="background-color: #D3D3D3" text-color="grey-9" label="Previous" class="q-ml-sm" icon="navigate_before"></q-btn>
          <q-btn @click="() => { done5 = true }" color="green" icon-right="check" label="Confirmer"></q-btn>
        </q-stepper-navigation>
      </q-step>
      
    </q-stepper>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data() {
    return {
        step: 1,
        done1: false,
        done2: false,
        done3: false,
        done4: false,
        stateForm1: false,
        stateForm2: false,
        fillInput: [],
        P1TypeInscription: '',
        typeInscription: [ 
          'En Ligne',
          'Présentiel',
          'Validée',
          'A confirmer'
        ],
        P1DateInscription: '',
        P1NomDeFamille: '',
        P1Prenom: '',
        P1BirthDate: '',
        P1Sexe: '',
        Sexe: [
          'Féminin',
          'Masculin',
          'Oui s\'il vous plaît !'
        ],
        P1LieuDeNaissance: '',
        P1Email: '',
        P1Telephone: '',
        P1Adresse: '',
        P1ClasseEnregistrement: '',
        ClasseEnregistrement: [
          '1',
          '2',
          '3',
          '4'
        ],
        P2TypeNotification: '',
        TypeNotification: [
          'Une',
          'Deux',
          'Trois',
          'Quatre'
        ],
        P2ActiviteExtraScolaire: null,
        ActiviteExtraScolaire: [
          'Football',
          'Handball',
          'Basketball',
          'Boxe Française',
          'Musique'
        ],
        P2ContactPerson: [
          {
            nom: '',
            prenom: '',
            email: '',
            telephone: ''
          }
        ],
        P2ContactData: [],
        P2ContactColumns: [
        {
          name: 'nom',
          required: true,
          label: 'Nom',
          align: 'left',
          field: 'nom',
          format: val => `${val}`,
          sortable: true
        },
        {
          name: 'prenom',
          required: true,
          label: 'Prénom(s)',
          align: 'left',
          field: 'prenom',
          format: val => `${val}`,
          sortable: true
        },
        {
          name: 'email',
          required: true,
          label: 'Email',
          align: 'left',
          field: 'email',
          format: val => `${val}`,
          sortable: true
        },
        {
          name: 'telephone',
          required: true,
          label: 'Téléphone',
          align: 'left',
          field: 'telephone',
          format: val => `${val}`,
          sortable: true
        },
        ],
        nom: '',
        prenom: '',
        email: '',
        telephone: '',
        P2GroupeSanguin: '',
        GroupeSanguin: [
          'A+',
          'A-',
          'B+',
          'B-',
          'AB+',
          'AB-',
          'O+',
          'O-'
        ],
        P2MaladieFrequente: '',
        P3TypePaiement: '',
        TypePaiement: [
          'Carte Bleue',
          'Virement Bancaire',
          'Mobile Money',
          'Espèces',
          'Chèque Bancaire',
          'Autre...'
        ],
        P3DispenseSport: true,
        P3ModalitePaiement: '',
        ModalitePaiement: [
          'Hebdomadaire',
          'Mensuel',
          'Trimestriel',
          'Bi-Annuel',
          'Annuel'
        ],
        P3Description: '',
        P4Observation: '',
    }
  },
  methods: {
    checkForm1() {
      if (this.$refs.myForm1) {
        this.$refs.myForm1.validate().then(success => {
          if (success) {
            this.stateForm1 = false;
            this.done1 = true;
            this.step = 2
          }
          else {
            this.stateForm1 = true;
            this.done1 = false;
            this.step = 1;
          }
        });
      }
    },

    populateContact() {
      this.P2ContactData.push({
        nom: `<q-input
                type="email"
                v-model="P1Email"
                autogrow
                label="Adresse Email"
              />`,
        prenom: '',
        email: '',
        telephone: '',
      })
      console.log(this.P2ContactData)
    },

    checkForm2() {

    },

    checkForm3() {

    },

    checkFile (files) {
      return files.filter(file => file.type === 'image/png') && files.filter(file => file.size < 2048000)
    },

    onRejected (rejectedEntries) {
      this.$q.notify({
        type: 'negative',
        message: `${rejectedEntries.length} file(s) did not pass validation constraints`
      })
    },


  }
}
</script>

<style>
.innerColumn{
  padding: 0.5rem 1rem 0.5rem 0rem;
}

.calendarRow {
  justify-content: space-between;
}

.dateShow {
  align-self: center;
  padding-right: 1rem;
}

button {
  margin: 0.3rem 0.5rem 1rem 0.5rem;
}
</style>