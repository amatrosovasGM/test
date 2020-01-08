<template>
  <div class="sidebar" :style="addedStyles">
    <h5>
      GOOD
      <br />MONDAY
    </h5>
    <nav class="sidebar-nav">
      <div
        class="menu-item"
        v-for="category in menuCategories"
        :key="category.category"
        :class="{ active: category.key === routePath }"
      >
        <div v-if="category.category" class="category">{{ category.category }}</div>

        <div v-for="item in category.items" :key="item.link">
          <a :href="'/' + item.link">
            <i
              :class="[
                item.key === routePath ? item.icon : `${item.icon}-outline`
              ]"
            />
            <p>{{ translate(item.key) }}</p>
          </a>
          <!-- <router-link :to="'/' + item.link">
            <i
              :class="[
                item.key === routePath ? item.icon : `${item.icon}-outline`
              ]"
            />
            <p>{{ translate(item.key) }}</p>
          </router-link>-->
        </div>
      </div>
    </nav>
  </div>
</template>

<script>
export default {
  name: "Sidebar",
  components: {},
  computed: {
    addedStyles() {
      return this.forceShow ? { display: "block" } : {};
    }
  },
  props: {
    menuCategories: {
      type: Array,
      required: true,
      default: () => []
    },
    forceShow: {
      type: Boolean,
      required: false,
      default: false
    },
    routePath: {
      type: String,
      required: true,
      default: ""
    },
    translate: {
      type: Function,
      required: true,
      default: () => {}
    }
  }
};
</script>

<style scoped lang="scss">
.sidebar {
  color: var(--primary);
  background-color: var(--boxBackground);
  padding: 20px 0 0 30px;
  height: 100%;

  h5 {
    font-weight: bold;
    margin-bottom: 20px;
  }
  .sidbar-nav {
    .active {
      svg,
      p {
        color: #e4613b;
      }
    }
  }
  .menu-item {
    cursor: pointer;
    font-size: 16px;
    :hover {
      color: var(--active);
      i {
        color: var(--active);
      }
    }
    .category {
      font-size: 12px;
      font-weight: bold;
      margin: 10px 0;
      color: var(--textPrimary);
    }
    a {
      display: -webkit-inline-box;
      text-decoration: none;
      color: var(--secondary);
      padding-top: 0px;
      &.router-link-exact-active {
        color: var(--active);
        i {
          color: var(--active);
        }
      }
      i {
        margin-top: 3px;
        color: var(--primary);
      }
      p {
        margin-left: 10px;
        margin-bottom: 5px;
      }
    }
  }
}
@media screen and (max-width: 768px) {
  .sidebar {
    display: none;
  }
}
</style>
