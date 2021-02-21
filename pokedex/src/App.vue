<script>
import DetalhePokemon from "./components/DetalhePokemon";
import Index from "./components/Index";

const routes = {
  "/": Index,
  "/detalhe": DetalhePokemon,
};

const NotFound = { template: "<p>Page not found</p>" };

export default {
  name: "App",
  data() {
    return {
      currentRoute: window.location.pathname,
    };
  },
  computed: {
    ViewComponent() {
      console.log("this.currentRoute", this.currentRoute);
      return routes[this.currentRoute] || NotFound;
    },
  },
  render(h) {
    return h(this.ViewComponent);
  },
};
</script>

