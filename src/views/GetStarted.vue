<template>
    <div class="getStarted">
        <NavBar/>
          <svg id="svg1" xmlns="http://www.w3.org/2000/svg" xml:lang="en"
            xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 500 500">
            <title>Cursor</title>
            <defs>
                <path id="textcircle"
                    d="M250,400
                        a150,150 0 0,1 0,-300a150,150 0 0,1 0,300Z"
                    transform="rotate(12,250,250)"/>
            </defs>
            <rect width="100%" height="100%" fill="none" />
            <text>
                <textPath xlink:href="#textcircle"
                        aria-label="All for One &amp; One for All"
                        textLength="942">GET STARTED TODAY .</textPath>
            </text>
        </svg>

        <div id="form">
        <b-form @submit="onSubmit" @reset="onReset">
        <b-form-group
            id="input-group-1"
            label="Company"
            label-for="input-1"
            description="Type your brand name if you don't have a company"
        >
            <b-form-input
            id="input-1"
            v-model="form.company"
            type="company"
            placeholder="Enter Company Name"
            required
            ></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-2" label="Your Name:" label-for="input-2">
            <b-form-input
            id="input-2"
            v-model="form.name"
            placeholder="Enter name"
            required
            ></b-form-input>
        </b-form-group>

         <b-form-group id="input-group-2" label="Your phone number" label-for="input-2">
            <b-form-input
            id="input-2"
            v-model="form.phone"
            placeholder="Enter your phone number"
            required
            ></b-form-input>
        </b-form-group>


        <b-button type="submit" variant="danger">Submit</b-button>

        </b-form>
         </div>
    </div>
</template>

<script>
import NavBar from "@/components/navbar.vue";

export default {
  name: "Home",
  components: {
    NavBar

  },

  data(){
    return{
        form: {
          company: '',
          name: '',
          phone:'',
        },
        show: true
      }
  },
     methods: {
      onSubmit(event) {
        event.preventDefault()

        this.$swal({
            icon: 'success',
            title: 'Thank You',
            text: 'One of our agents will contact you soon',
        });
      },
      onReset(event) {
        event.preventDefault()
        // Reset our form values
        this.form.company = ''
        this.form.name = ''
        this.form.phone = ''

        // Trick to reset/clear native browser form validation state
        this.show = false
        this.$nextTick(() => {
          this.show = true
        })
      }
    },

      mounted(){
            const circleSvg = document.getElementById('svg1')

            let mouseX = 0
            let mouseY = 0
            window.addEventListener('mousemove', (event) => {
                mouseY = (event.clientY / 16) - (45 / 16) + 'rem'
                mouseX = (event.clientX / 16) - (45 / 16) + 'rem'
            })
            const mouseMove = () => {
                circleSvg.style.top = mouseY
                circleSvg.style.left = mouseX
                window.requestAnimationFrame(mouseMove)
            }
            mouseMove()
        }
}
</script>



<style scoped>
#form{
    margin-top: 10%;
    margin-inline: auto;
    min-width: 210px;
    max-width: 20%;
}


  svg {
    width: 100px;
    position: absolute;
    animation: rotation 4.5s infinite linear;
    pointer-events: none;
    transition: top 1s, left 1s;
    transition-timing-function: ease-out;
    z-index: 9999;
  }
h2{
 font-family: 'Poppins';
    font-style: oblique;
    font-size: 2.5em;
    color: #D33F49;
}

p{
 font-family: 'Poppins';
    font-style: italic;
    font-size: 1.5em;
    color: #D33F49;
}
  text{
    font-family: 'Poppins';
    font-style: italic;
    font-size: 4.5em;
    fill: #D33F49;
  }

  @keyframes rotation {
    from {
      transform: rotate(359deg);
    }
    to {
      transform: rotate(0deg);
    }
}

</style>