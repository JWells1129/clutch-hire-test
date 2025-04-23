<template>
  <div class="about">
    <h1></h1>

    <div v-if="submitted" class="thank-you-message">
      <p>Thank you</p>
      <p>We will contact you shortly</p>
    </div>

    <form v-else @submit.prevent="submitForm">
      <div>
        <h1>Have us reach out</h1>
      </div>

      <div>
        <label for="first">First Name</label>
        <input type="text" id="first" v-model="form.first" required />
      </div>

      <div>
        <label for="last">Last Name</label>
        <input type="text" id="last" v-model="form.last" required />
      </div>

      <div>
        <label for="company">Company</label>
        <input type="text" id="company" v-model="form.company" required />
      </div>

      <div>
        <label for="phone">Phone</label>
        <input type="text" id="phone" v-model="form.phone" required />
      </div>

      <div>
        <label for="email">Email</label>
        <input type="email" id="email" v-model="form.email" required />
      </div>

      <button type="submit">Continue</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        first: "",
        last: "",
        company: "",
        phone: "",
        email: "",
      },
      submitted: false,
    };
  },
  methods: {
    async submitForm() {
      const apiUrl = `https://dev-api-api.hiring-test.experientialpreview.com/api/lead/aed6a007-b0f7-4dc0-bb42-be1122f56b76`;

      const formRequest = {
        first: this.form.first,
        last: this.form.last,
        company: this.form.company,
        phone: this.form.phone,
        email: this.form.email,
      };

      try {
        const response = await fetch(apiUrl, {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify(formRequest),
        });

        if (response.ok) {
          this.submitted = true;
          setTimeout(() => {
            this.resetForm();
          }, 5000);
        } else {
          alert("Error submitting form.");
        }
      } catch (error) {
        console.error("Error:", error);
      }
    },
    resetForm() {
      this.form.first = "";
      this.form.last = "";
      this.form.company = "";
      this.form.phone = "";
      this.form.email = "";
      this.submitted = false;
    },
  },
};
</script>

<style scoped>
.about {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  padding: 20px;
}

form {
  max-width: 300px;
  width: 100%;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  transition: width 0.3s ease, padding 0.3s ease;
}

form div {
  margin-bottom: 15px;
}

label {
  display: block;
  margin-bottom: 5px;
  font-size: 16px;
  color: green;
}

input {
  width: 100%;
  padding: 8px 0px;
  margin-top: 5px;
  border-radius: 4px;
  border: 1px solid #ccc;
  font-size: 14px;
}

button {
  padding: 12px 20px;
  background-color: rgb(5, 62, 122);
  color: white;
  border: none;
  cursor: pointer;
  border-radius: 4px;
  font-size: 16px;
  width: auto;
  display: block;
  margin-left: auto;
}

button:hover {
  background-color: #0056b3;
}

h1 {
  margin-bottom: 20px;
  text-align: left;
  font-size: 20px;
  color: gray;
}

.thank-you-message {
  margin-top: 20px;
  text-align: center;
  font-size: 18px;
}

/* Adjust parameters for 393 x 852 resolution */
@media (max-width: 393px) and (max-height: 852px) {
  .about {
    padding: 10px;
    font-family: "Arial", sans-serif;
  }

  form {
    max-width: 100%;
    padding: 15px 20px;
    box-shadow: none;
  }

  input,
  button {
    margin-right: 10px;
    font-size: 14px;
  }

  label {
    font-size: 14px;
    word-wrap: break-word;
    word-break: break-word;
    white-space: normal;
    color: green;
  }

  .thank-you-message {
    font-size: 16px;
    color: gray;
  }
}
</style>
