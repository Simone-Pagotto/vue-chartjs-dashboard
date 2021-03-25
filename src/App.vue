<template>
  <div id="app">
    <div class="sidebar">
      <div class="title">- Dashbool -</div>
      <div class="avatar">
        <div class="circle"></div>
        <div class="info">
          <p>Welcome</p>
          <p class="name">Mario Rossi</p>
        </div>
      </div>
      <div class="general">GENERAL</div>
      <ul class="list">
        <li>
          <div class="list-head">
            <div>
              <i class="fa fa-home" aria-hidden="true"></i>
              <p>Home</p>
            </div>
            <i
              @click="toggleMenu"
              :class="isOpen ? 'fa fa-chevron-up' : 'fa fa-chevron-down'"
              aria-hidden="true"
            >
            </i>
          </div>
          <ul class="sub-list" :style="isOpen ? ' ' : 'display: none;'">
            <li>Dasboard</li>
            <li>Dasboard</li>
            <li>Dasboard</li>
          </ul>
        </li>
        <li>
          <div class="list-head">
            <div>
              <i class="fa fa-map" aria-hidden="true"></i>
              <p>Maps</p>
            </div>
            <i class="fa fa-chevron-down" aria-hidden="true"></i>
          </div>
          <ul class="sub-list">
            <li>Dasboard</li>
            <li>Dasboard</li>
            <li>Dasboard</li>
          </ul>
        </li>
        <li>
          <div class="list-head">
            <div>
              <i class="fa fa-cog" aria-hidden="true"></i>
              <p>Config</p>
            </div>
            <i class="fa fa-chevron-down" aria-hidden="true"></i>
          </div>
          <ul class="sub-list">
            <li>Dasboard</li>
            <li>Dasboard</li>
            <li>Dasboard</li>
          </ul>
        </li>
        <li>
          <div class="list-head">
            <div>
              <i class="fa fa-envelope" aria-hidden="true"></i>
              <p>Contacts</p>
            </div>
            <i class="fa fa-chevron-down" aria-hidden="true"></i>
          </div>
          <ul class="sub-list">
            <li>Dasboard</li>
            <li>Dasboard</li>
            <li>Dasboard</li>
          </ul>
        </li>
      </ul>
    </div>
    <div class="stage"></div>
  </div>
</template>

<script>
//import Vue from "vue";
export default {
  data() {
    return {
      isOpen: false,
    };
  },
  methods: {
    toggleMenu: function () {
      this.isOpen = !this.isOpen;
    },
  },
};
</script>

<style lang="scss">
@import "./scss/commons.scss";
#app {
  width: 100vw;
  height: 100vh;
  display: flex;
  .sidebar {
    width: $sb-w;
    background-color: $primary-color;
    color: $white;
    padding: 1rem 0.5rem;
    display: flex;
    flex-direction: column;
    .title {
      font-size: 1.2rem;
      font-weight: 700;
      margin-bottom: 1rem;
    }
    .avatar {
      display: flex;
      align-items: center;
      margin-bottom: 1rem;
      .circle {
        width: 3rem;
        height: 3rem;
        border-radius: 50%;
        background-color: $white;
      }
      .info {
        margin-left: 1rem;
        p {
          font-size: 1rem;
        }
        .name {
          font-size: 0.8rem;
          font-weight: 700;
        }
      }
    }
    .general {
      font-size: 1rem;
      font-weight: 700;
      margin-bottom: 1rem;
    }
    .list {
      border-top: 0.2rem solid;
      .list-head {
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding-top: 1rem;
        div {
          display: flex;
          flex-direction: row;
          align-items: center;
          p {
            margin-left: 1rem;
            font-size: 1.2rem;
            font-weight: 300;
          }
        }
      }
      .sub-list {
        margin-top: 0.3rem;
        list-style: none;
        li {
          padding: 0.1rem 0;
          padding-left: 2rem;
          font-size: 0.8rem;
          font-weight: 300;
          &:hover {
            background-color: $secondary-color;
          }
        }
      }
    }
  }
  .stage {
    width: $stage-w;
    background-color: $light-color;
  }
}
</style>
