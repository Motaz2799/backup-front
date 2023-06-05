<template>
  <div class="container-fluid mt-4 mt-4">
    <div v-if="!assessmentCompleted" class="alert alert-warning" role="alert">
        <span class="alert-icon"><span class="visually-hidden">Warning</span></span>
        Please complete the assessment for a better evaluation
        </div>
        <div class="row mb-5">
        <div class="col-md-6">

        <caption class="wide-column">
          <div>{{ appName }}</div>
          <div class="btn-group dropend">
            <button
              type="button"
              class="menuItem-active-link btn btn-sm btn-secondary dropdown-toggle"
              data-bs-toggle="dropdown"
              aria-expanded="false"
            >
              Export
            </button>
            <ul class="dropdown-menu">
              <li>
                <a
                  class="dropdown-item"
                  type="button"
                  data-bs-toggle="modal"
                  data-bs-target="#exampleModalToggle"
                  @click="onclickDownoaldPdf"
                >
                  PDF
                </a>
              </li>
              <li>
                <a
                  class="dropdown-item"
                  type="button"
                  data-bs-toggle="modal"
                  data-bs-target="#exampleModalToggleDB"
                  @click="onclickDownoaldWord"
                >
                  WORD
                </a>
              </li>
            </ul>
          </div>
        </caption>
        <h6 class="text-muted">{{ appDescription }}</h6>
        
        
        <div class="card">
          <div class="card-header">Contacts</div>
        <div class="card-body" v-for="contact in contacts" :key="contact.id">{{ contact.fullName }} - {{ contact.title }}-{{ contact.email }}</div>
        </div>
                
      </div>

      <!-- <div  v-if="serversCount === 0" class="alert alert-warning alert-sm" role="alert">
  <span class="alert-icon"><span class="visually-hidden">Warning</span></span>
  <p>No servers available for this application.</p>
</div>

<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-hdd-rack" viewBox="0 0 16 16">
          <path d="M4.5 5a.5.5 0 1 0 0-1 .5.5 0 0 0 0 1zM3 4.5a.5.5 0 1 1-1 0 .5.5 0 0 1 1 0zm2 7a.5.5 0 1 1-1 0 .5.5 0 0 1 1 0zm-2.5.5a.5.5 0 1 0 0-1 .5.5 0 0 0 0 1z"/>
          <path d="M2 2a2 2 0 0 0-2 2v1a2 2 0 0 0 2 2h1v2H2a2 2 0 0 0-2 2v1a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2v-1a2 2 0 0 0-2-2h-1V7h1a2 2 0 0 0 2-2V4a2 2 0 0 0-2-2H2zm13 2v1a1 1 0 0 1-1 1H2a1 1 0 0 1-1-1V4a1 1 0 0 1 1-1h12a1 1 0 0 1 1 1zm0 7v1a1 1 0 0 1-1 1H2a1 1 0 0 1-1-1v-1a1 1 0 0 1 1-1h12a1 1 0 0 1 1 1zm-3-4v2H4V7h8z"/>
        </svg> Servers: {{ serversCount }} -->
      <div class="col-md-4" style="padding-left: 150px;">
        <div class="card" style="width: 15.2rem">
          <div class="card-header">Insights</div>
          <ul class="list-group list-group-flush">
            
            <li
              class="list-group-item"
              v-if="serversCount === 0"
              style="padding-top: 8px;padding-bottom: 8px;width: 240px;height: 56px;padding-left: 13px;"
            >
              <div class="alert alert-warning alert-sm" role="alert">
                <span class="alert-icon" style="padding-left: 0px"
                  ><span class="visually-hidden">Warning</span></span
                ><span
                  ><p
                    style="
                      padding-left: 5px;
                      font-size: large;
                      width: 170px;
                      font-weight: 600;
                      padding-top: 1px;
                    "
                  >
                    Linked Servers
                  </p></span
                ><span style="padding-left: 0px"><p style="margin: 0;font-size: x-large;font-weight: 700;">{{ serversCount }}</p></span
                >
              </div>
            </li>

            <li
              class="list-group-item"
              v-else
              style="padding-top: 8px;padding-bottom: 8px;width: 240px;height: 56px;padding-left: 13px;"
            >
              <div class="alert alert-success alert-sm" role="alert">
                <span class="alert-icon" style="padding-left: 0px"
                  ><span class="visually-hidden">Warning</span></span
                ><span
                  ><p
                    style="
                      padding-left: 5px;
                      font-size: large;
                      width: 170px;
                      font-weight: 600;
                      padding-top: 1px;
                    "
                  >
                    Linked Servers
                  </p></span
                ><span style="padding-left: 0px"
                  ><p style="margin: 0;font-size: x-large;font-weight: 700;">{{ serversCount }}</p></span
                >
              </div>
            </li>

            <li
              class="list-group-item"
              v-if="databasesCount === 0"
              style="padding-top: 8px;padding-bottom: 8px;width: 240px;height: 56px;padding-left: 13px;"
            >
              <div class="alert alert-warning alert-sm" role="alert">
                <span class="alert-icon" style="padding-left: 0px"
                  ><span class="visually-hidden">Warning</span></span
                ><span
                  ><p
                    style="
                      padding-left: 5px;
                      font-size: large;
                      width: 170px;
                      font-weight: 600;
                      padding-top: 1px;
                    "
                  >
                    Linked Databases
                  </p></span
                ><span style="padding-left: 0px"
                  ><p style="margin: 0;font-size: x-large;font-weight: 700;">{{ databasesCount }}</p></span
                >
              </div>
            </li>

            <li
              class="list-group-item"
              v-else
              style="padding-top: 8px;padding-bottom: 8px;width: 240px;height: 56px;padding-left: 13px;"
            >
              <div class="alert alert-success alert-sm" role="alert">
                <span class="alert-icon" style="padding-left: 0px"
                  ><span class="visually-hidden">Warning</span></span
                ><span
                  ><p
                    style="
                      padding-left: 5px;
                      font-size: large;
                      width: 170px;
                      font-weight: 600;
                      padding-top: 1px;
                    "
                  >
                    Linked Databases
                  </p></span
                ><span style="padding-left: 0px"
                  ><p style="margin: 0;font-size: x-large;font-weight: 700;">{{ databasesCount }}</p></span
                >
              </div>
            </li>

            <li
              class="list-group-item"
              v-if="interfacesCount === 0"
              style="padding-top: 8px;padding-bottom: 8px;width: 240px;height: 56px;padding-left: 13px;"
            >
              <div class="alert alert-warning alert-sm" role="alert">
                <span class="alert-icon" style="padding-left: 0px"
                  ><span class="visually-hidden">Warning</span></span
                ><span
                  ><p
                    style="
                      padding-left: 5px;
                      font-size: large;
                      width: 170px;
                      font-weight: 600;
                      padding-top: 1px;
                    "
                  >
                    Linked Interfaces
                  </p></span
                ><span style="padding-left: 0px"
                  ><p style="margin: 0;font-size: x-large;font-weight: 700;">{{ interfacesCount }}</p></span
                >
              </div>
            </li>

            <li
              class="list-group-item"
              v-else
              style="padding-top: 8px;padding-bottom: 8px;width: 240px;height: 56px;padding-left: 13px;"
            >
              <div class="alert alert-success alert-sm" role="alert">
                <span class="alert-icon" style="padding-left: 0px"
                  ><span class="visually-hidden">Warning</span></span
                ><span
                  ><p
                    style="
                      padding-left: 5px;
                      font-size: large;
                      width: 170px;
                      font-weight: 600;
                      padding-top: 1px;
                    "
                  >
                    Linked Interfaces
                  </p></span
                ><span style="padding-left: 0px"
                  ><p style="margin: 0;font-size: x-large;font-weight: 700;">{{ interfacesCount }}</p></span
                >
              </div>
            </li>
          </ul>
        </div>
      </div>
    </div>
    
<!-- <button type="button" class="btn btn-secondary" data-bs-toggle="tooltip" data-bs-placement="top" data-bs-custom-class="custom-tooltip" data-bs-title="This top tooltip is themed via CSS variables.">
      Custom tooltip
    </button> -->

    <div>

      <div v-if="ShowEvaluate===false" class="card w-50">
      <div class="card-body">
        <h5 class="card-title">Evaluate application</h5>
        <p class="card-text">With supporting text below as a natural lead-in to additional content.</p>
        <button  type="button" @click="getEvaluation" class="menuItem-active-link btn btn-sm btn-secondary">
          Evaluate Application 
      </button>
    </div>
    </div>
    </div>

      <div class="card text-center" v-if="ShowRecommandation">
      <div class="card-header">
        Recommended Strategy
      </div>
      <div class="card-body">
        <h5 class="card-title">{{ recommendedStrategy[0].key }}</h5>
        <p class="card-text">{{ recommendedStrategy[0].value}}</p>
        <button type="button" @click="fetchButtonImage" v-if="ShowImage===false" class="menuItem-active-link btn btn-sm btn-secondary">
          Show more details
        </button>  
        <img v-if="ShowImage" :src="Image" alt="Strategy" style="max-width: 100%; height: auto;" />  
        <div v-if="ShowImage" class="tab-content border-left-0 border-right-0 border-bottom-0">
      <div class="tab-pane active" id="help" role="tabpanel" tabindex="0" aria-hidden="false" aria-labelledby="tab991750">
        <p>From this view, you can edit or delete entry of your web site. You can also add an entry by clicking on "Add news" button.</p>
        <p>You can reorder column by clicking on them.</p>
        <p>Finally, you can search an item by typing his title or his ID in the search field, at the top of the page.</p>
      </div>
    </div>
      </div>
    </div>
    <br><br><br><br>
  </div>
 
</template>

<script>
import axios from 'axios'




export default {
  props: {
    id: Number,
    appName: {
      type: String,
      required: true
    }
  },

  
  
  data() {
    return {
      showMessage: false,
      showContacts: true,
      showServers: false,
      appDescription: '',
      servers: [],
      contacts: [],
      Image: null,
      serversCount: null,
      databasesCount: null,
      interfacesCount: null,
      assessmentCompleted: true,
      ShowImage: false,
      ShowEvaluate:false,
      ShowRecommandation:false,
      recommendedStrategy:{}
    }
  },

  mounted() {
    axios
      .all([
        axios.get(`http://localhost:8080/api/v1/applications/${this.id}/servers`),
        axios.get(`http://localhost:8080/api/v1/applications/${this.id}/databases`),
        axios.get(`http://localhost:8080/api/v1/applications/${this.id}/interfaces`),
        axios.get(`http://localhost:8080/api/v1/applications/${this.id}`),
        axios.get(`http://localhost:8080/api/v1/applications/${this.id}/assessment`)
      ])
      .then(
        axios.spread(
          (
            serversResponse,
            databasesResponse,
            interfacesResponse,
            applicationResponse,
            assessmentResponse
          ) => {
            this.serversCount = serversResponse.data.length
            this.databasesCount = databasesResponse.data.length
            this.interfacesCount = interfacesResponse.data.length

            const applicationData = applicationResponse.data
            this.appDescription = applicationData.appDescription
            this.servers = applicationData.servers
            console.log(this.servers)
            this.contacts = applicationData.contacts
            this.assessmentCompleted = assessmentResponse.data.isCompleted
          }
        )
      )
      .catch((error) => {
        console.error(error)
      })
  },
  methods: {    
    getEvaluation() {
      axios.get(`http://localhost:5000/api/v1/strategy/${this.id}/non-detailed`) 
        .then(response => {
          const data = response.data;

          this.recommendedStrategy = Object.keys(data).map(key => {
            return { key, value: data[key] };
          });
          this.ShowRecommandation=true
          this.ShowEvaluate=true
          console.log(this.recommendedStrategy)
        })
        .catch(error => {
          console.error(error);
        });
    },
    
    fetchButtonImage() {
      axios
        .get(`http://localhost:5000/api/v1/strategy/${this.id}/detailed`, {
          responseType: 'arraybuffer'
        })
        .then((response) => {
          const base64Image = btoa(
            new Uint8Array(response.data).reduce(
              (data, byte) => data + String.fromCharCode(byte),
              ''
            )
          )
          this.Image = `data:image/png;base64, ${base64Image}`
          this.ShowImage = true
        })
        .catch((error) => {
          console.error("Erreur lors de la récupération de l'image", error)
        })
    },
    onclickDownoaldPdf() {
      fetch(`http://127.0.0.1:5000/api/v1/generate_report/${this.id}/pdf`, {
        method: 'GET',
        headers: {
          'Content-Type': 'application/pdf'
        }
      })
        .then((response) => response.blob())
        .then((blob) => {
          const url = window.URL.createObjectURL(blob)
          const link = document.createElement('a')
          link.href = url
          link.target = '_blank'
          link.download = `${this.appName}.pdf`
          link.click()
        })
        .catch((error) => {
          console.error('Erreur lors du téléchargement du PDF', error)
        })
    },
    
    onclickDownoaldWord() {
      fetch(`http://127.0.0.1:5000/api/v1/generate_report/${this.id}/word`, {
        method: 'GET',
        headers: {
          'Content-Type': 'application/vnd.openxmlformats-officedocument.wordprocessingml.document'
        }
      })
        .then((response) => response.blob())
        .then((blob) => {
          const url = window.URL.createObjectURL(blob)
          const link = document.createElement('a')
          link.href = url
          link.target = '_blank'
          link.download = `${this.appName}.docx`
          link.click()
        })
        .catch((error) => {
          console.error('Erreur lors du téléchargement du document Word', error)
        })
    }
  }
}


</script>

<style>
.wide-column {
  display: flex;
  align-items: center;
}

.image-container {
  height: 200px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.image-container img {
  max-width: 100%;
  max-height: 150%;
  object-fit: contain;
}

.dialog {
    position: relative;
    display: inline-block;
    padding: 10px;
    border-radius: 5px;
    background-color: #343a40;
    color: #000;
  }

  .dialog:before {
    content: "";
    position: absolute;
    top: -10px;
    left: 50%;
    margin-left: -10px;
    border-width: 10px;
    border-style: solid;
    border-color: transparent transparent #343a40 transparent;
  }

</style>
