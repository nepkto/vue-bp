<template>
  <!-- Main Sidebar Container -->
  <aside class="main-sidebar sidebar-dark-primary elevation-4">
    <!-- Brand Logo -->
    <a href="index3.html" class="brand-link">
      <img
        src="../../assets/rolling-nexus.png"
        alt="Rolling Nexus"
        class="brand-image img-circle elevation-3"
        style="opacity: 0.8"
      />
      <span class="brand-text font-weight-light">RN</span>
    </a>

    <!-- Sidebar -->
    <div class="sidebar">
      <!-- Sidebar user panel (optional) -->
      <div class="user-panel mt-3 pb-3 mb-3 d-flex">
        <div class="image">
          <img
            src="../../assets/img/user2-160x160.jpg"
            class="img-circle elevation-2"
            alt="User Image"
          />
        </div>
        <div class="info">
          <a href="#" class="d-block">{{ this.$store.state.auth.user.name }}</a>
        </div>
      </div>

      <!-- SidebarSearch Form -->
      <div class="form-inline">
        <div class="input-group" data-widget="sidebar-search">
          <input
            class="form-control form-control-sidebar"
            type="search"
            placeholder="Search"
            aria-label="Search"
          />
          <div class="input-group-append">
            <button class="btn btn-sidebar">
              <i class="fas fa-search fa-fw"></i>
            </button>
          </div>
        </div>
      </div>

      <!-- Sidebar Menu -->
      <nav class="mt-2">
        <ul
          class="nav nav-pills nav-sidebar flex-column"
          data-widget="treeview"
          role="menu"
          data-accordion="false"
        >
          <!-- Add icons to the links using the .nav-icon class
               with font-awesome or any other icon font library -->
          <li class="nav-item">
            <router-link :to="{ name: 'dashboard' }" class="nav-link"
              ><i class="nav-icon fas fa-th"></i>Dashboard</router-link
            >
          </li>
          <li class="nav-item">
            <a href="#" class="nav-link">
              <i class="nav-icon fas fa-tachometer-alt"></i>
              <p>
                System
                <i class="right fas fa-angle-left"></i>
              </p>
            </a>
            <ul class="nav nav-treeview">
              <li class="nav-item" v-if="authorizations.moduleAccess('User','read')">
                <router-link :to="{ name: 'user.index' }" class="nav-link"
                  ><i class="far fa-user nav-icon"></i>Users</router-link
                >
              </li>
              <li class="nav-item">
                <a href="#" class="nav-link">
                  <i class="far fa-users nav-icon"></i>
                  <p>Users Group</p>
                </a>
              </li>
            </ul>
          </li>
          <li class="nav-item">
            <a href="#" class="nav-link">
              <i class="nav-icon fas fa-th"></i>
              <p>
                Upgrade Request
                <span class="right badge badge-danger">0</span>
              </p>
            </a>
          </li>
        </ul>
      </nav>
      <!-- /.sidebar-menu -->
    </div>
    <!-- /.sidebar -->
  </aside>
</template>

<script>
import Authorizations from "@/helpers/Authorization";
export default {
  data() {
    return {
      // menuActive:false,
      authorizations: new Authorizations(),
    };
  },
  mounted() {
    const permissions = this.$store.state.auth.permissions || []
    const userGroup = this.$store.state.auth.user.group_name || ''
    this.authorizations.set(userGroup, permissions);
  },
};
</script>