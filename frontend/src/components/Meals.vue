<template>
  <b-container>
    <div v-if="meals.length">
      <b-row>
        <div :key="meal.index" v-for="meal in meals">
          <b-col l="4">
            <b-card
              :img-src="`http://localhost:1337${meal.image.url}`"
              :title="meal.title"
              img-alt="Image"
              img-top
              tag="article"
              style="max-width:25vw;height:10vw"
              class="mb-2"
            >
              <b-row>
                <b-card-text>{{ `${meal.description}` }}</b-card-text>
                <span>
                  <strong>Price: ${{ `${meal.price}` }} </strong>
                </span>
              </b-row>
              <b-row>
                <b-button @click="placeOrder" variant="primary">Order meal</b-button>
              </b-row>
            </b-card>
          </b-col>
        </div>
      </b-row>
    </div>
    <div v-else>
      <h5>Fetching meals . . .</h5>
    </div>
  </b-container>
</template>
<script>
export default {
  data() {
    return {
      meals: [],
    };
  },
  mounted() {
    fetch("http://localhost:1337/products")
      .then((res) => res.json())
      .then((data) => {
          console.log(data)
        this.meals = data;
      });
  }
};
</script>