<template>
  <transition
    mode="out-in"
    class="animate__animated"
    :class="open ? 'animate__fadeInLeftBig' : null"
  >
    <div>
      <aside class="side-bar" :class="open ? 'active' : null">
        <div class="container-fluid">
          <div class="row heading my-2 px-3 py-3">
            <div class="col-12">
              <h6 class="nav-header">My <span>App </span></h6>
            </div>
          </div>
          <hr class="divider" />
          <ul class="navbar-nav mt-3">
            <li class="nav-item">
              <router-link to="/dashboard" class="nav-link">
                <box-icon
                  name="message-square"
                  type="solid"
                  :animation="IconConfig.animation"
                  :color="IconConfig.color"
                  :size="IconConfig.size"
                ></box-icon>

                <span>Dashboard</span>
              </router-link>
            </li>

            <template v-if="user.role == 'ADMIN'">
              <li class="nav-item">
                <router-link
                  to="/dashboard/add-bulk-data/teacher"
                  class="nav-link"
                >
                  <box-icon
                    name="data"
                    :animation="IconConfig.animation"
                    :color="IconConfig.color"
                    :size="IconConfig.size"
                  ></box-icon>
                  <span>Bulk Teacher Data</span>
                </router-link>
              </li>
              <li class="nav-item">
                <router-link
                  to="/dashboard/add-bulk-data/student"
                  class="nav-link"
                >
                  <box-icon
                    name="data"
                    :animation="IconConfig.animation"
                    :color="IconConfig.color"
                    :size="IconConfig.size"
                  ></box-icon>
                  <span>Bulk Student Data</span>
                </router-link>
              </li>
              <li class="nav-item">
                <router-link to="/dashboard/add-section" class="nav-link">
                  <box-icon
                    name="building"
                    :animation="IconConfig.animation"
                    :color="IconConfig.color"
                    :size="IconConfig.size"
                  ></box-icon>
                  <span>Add Sections</span>
                </router-link>
              </li>
              <li class="nav-item">
                <router-link to="/dashboard/add-teacher" class="nav-link">
                  <box-icon
                    name="user-plus"
                    :animation="IconConfig.animation"
                    :color="IconConfig.color"
                    :size="IconConfig.size"
                  ></box-icon>
                  <span>Add Teacher</span>
                </router-link>
              </li>
              <li class="nav-item">
                <router-link to="/dashboard/add-admin" class="nav-link">
                  <box-icon
                    name="user-check"
                    :animation="IconConfig.animation"
                    :color="IconConfig.color"
                    :size="IconConfig.size"
                  ></box-icon>
                  <span>Add Admin</span>
                </router-link>
              </li>
            </template>
            <template v-if="user.role == 'SECTION_HEAD'">
              <li class="nav-item">
                <router-link to="/dashboard/add-class" class="nav-link">
                  <box-icon
                    name="layer-plus"
                    :animation="IconConfig.animation"
                    :color="IconConfig.color"
                    :size="IconConfig.size"
                  ></box-icon>
                  <span>Add Classes</span>
                </router-link>
              </li>
            </template>
            <template v-if="user.role == 'TEACHER'">
              <li class="nav-item">
                <router-link to="/dashboard/assign-students" class="nav-link">
                  <box-icon
                    name="duplicate"
                    :animation="IconConfig.animation"
                    :color="IconConfig.color"
                    :size="IconConfig.size"
                  ></box-icon>
                  <span>Assign Students</span>
                </router-link>
              </li>
              <li class="nav-item">
                <router-link to="/dashboard/add-students" class="nav-link">
                  <box-icon
                    name="user-plus"
                    :animation="IconConfig.animation"
                    :color="IconConfig.color"
                    :size="IconConfig.size"
                  ></box-icon>
                  <span>Add Students</span>
                </router-link>
              </li>
              <li class="nav-item">
                <router-link to="/dashboard/attendance" class="nav-link">
                  <box-icon
                    name="calendar-check"
                    :animation="IconConfig.animation"
                    :color="IconConfig.color"
                    :size="IconConfig.size"
                  ></box-icon>
                  <span>Student Attendance</span>
                </router-link>
              </li>
              <li class="nav-item">
                <router-link
                  to="/dashboard/attendance-history"
                  class="nav-link"
                >
                  <box-icon
                    name="history"
                    :animation="IconConfig.animation"
                    :color="IconConfig.color"
                    :size="IconConfig.size"
                  ></box-icon>
                  <span>Attendance History</span>
                </router-link>
              </li>
              <li class="nav-item">
                <router-link
                  to="/student/attendance/percentage"
                  class="nav-link"
                >
                  <box-icon
                    name="pie-chart-alt"
                    type="solid"
                    :animation="IconConfig.animation"
                    :color="IconConfig.color"
                    :size="IconConfig.size"
                  ></box-icon>

                  <small>Attendance Percentage</small>
                </router-link>
              </li>
            </template>
            <hr class="divider</hr>" />

            <li class="nav-item">
              <router-link to="/dashboard/account" class="nav-link">
                <box-icon
                  name="user"
                  type="solid"
                  :animation="IconConfig.animation"
                  :color="IconConfig.color"
                  :size="IconConfig.size"
                ></box-icon>
                <span>Account Details</span>
              </router-link>
            </li>
            <li class="nav-item">
              <router-link to="/dashboard/logout" class="nav-link">
                <box-icon
                  name="exit"
                  :color="IconConfig.color"
                  :size="IconConfig.size"
                >
                </box-icon>

                <span>Sign Out</span>
              </router-link>
            </li>
            <hr class="divider" />
          </ul>
        </div>
      </aside>
    </div>
  </transition>
</template>

<script>
import { mapGetters } from "vuex";
import "boxicons";
export default {
  computed: mapGetters({
    user: "auth/GET_USER",
  }),
  props: {
    open: {
      type: Boolean,
    },
  },
  data() {
    return {
      IconConfig: {
        animation: "",
        color: "#f8bf06",
        size: "bx-sm",
      },
    };
  },
};
</script>

<style lang="scss" scoped>
// 768px
aside {
  min-width: 250px;
  width: 250px;
  height: 100%;
  overflow-x: hidden;
  overflow-y: auto;
  background: var(--dashboard-color);
  display: block;
  margin: auto 0;
  z-index: 999;

  hr {
    background: var(--dashboard-main);
  }

  .heading {
    .nav-header {
      font-weight: 900;
      color: var(--dashboard-main);
      text-transform: uppercase;
      text-align: center;
    }
  }

  ul {
    li {
      transition: all 0.5s ease-in-out;
      border-radius: 10px;

      &:hover {
        background: var(--dashboard-color-light);
      }

      .nav-link {
        width: 90%;
        height: 100%;
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 1rem;
        font-size: 14px;
        font-weight: 600;
        color: var(--dashboard-main);
      }

      .router-link-active {
        font-weight: 900;
      }
    }
  }
}

@media screen and (max-width: 768px) {
  div {
    z-index: 99999;

    aside {
      position: fixed;
      top: 0;
      left: 0;
      display: none;
      z-index: 99999;

      &:is(.active) {
        display: block;
        z-index: 99999;
      }
    }
  }
}

@media screen and (max-width: 300px) {
  aside {
    min-width: 200px;
    width: 200px;

    ul {
      li {
        .nav-link {
          width: 100%;
          font-size: 10px;
        }
      }
    }
  }
}
</style>
