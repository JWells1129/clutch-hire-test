<template>
  <div class="about">
    <h1></h1>

    <div v-if="submitted" class="thank-you-message">
      <p>Thank you!</p>
    </div>

    <form v-else @submit.prevent="submitForm">
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

      <button type="submit">Submit</button>
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
          }, 5000); // Reset after 5 seconds
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
  flex-direction: column;
}

form {
  max-width: 300px;
  width: 100%;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

form div {
  margin-bottom: 15px;
}

label {
  display: block;
  margin-bottom: 5px;
}

input {
  width: 100%;
  padding: 8px;
  margin-top: 5px;
  border-radius: 4px;
  border: 1px solid #ccc;
}

button {
  padding: 10px 15px;
  background-color: #007bff;
  color: white;
  border: none;
  cursor: pointer;
  border-radius: 4px;
  width: 100%;
}

button:hover {
  background-color: #0056b3;
}

.thank-you-message {
  font-size: 18px;
  color: green;
  text-align: center;
  padding: 20px;
  background-color: #f4f4f4;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  width: 300px;
}

form {
  display: block;
}

form.v-enter,
.form.v-leave {
  display: none;
}
</style>
