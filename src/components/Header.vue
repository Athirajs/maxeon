<template>
  <div>
    <div class="header">
      <div class="nav">
        <input type="checkbox" id="nav-check" />
        <div class="nav-header">
          <div class="nav-title">Maxeon</div>
        </div>
        <div class="nav-btn">
          <label for="nav-check">
            <span></span>
            <span></span>
            <span></span>
          </label>
        </div>

        <div class="nav-links">
          <a href="#">Products</a>
          <a href="#">Features</a>
          <a href="#">Use Cases</a>
          <a href="#">Pricing</a>
          <a class="login" href="#">Login</a>
        </div>
      </div>
      <section class="center-div">
        <div class="main-heading">
          <h1>Where words fail, Music speaks.</h1>
        </div>
      </section>
    </div>
  </div>
</template>
<script>
export default {};
</script>
<style lang="scss" scoped >
$blue-violet: "#7F8AC5";
$light-green: "#13A884";
$blue: "#4C5AA1";
$rose-white: "#ECF1FB";
$dark-blue: "#0C003A";
.header {
  width: 100%;
  height: 100vh;
  background: url("../img/Banner.png");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
  position: relative;
}

.nav {
  height: 50px;
  width: 100%;
  position: relative;
  padding: 30px 100px 0 50px;
}

.nav > .nav-header {
  display: inline;
}

.nav > .nav-header > .nav-title {
  display: inline-block;
  font-size: 45px;
  color: #ecf1fb;
  font-weight: 600;
}

.nav > .nav-btn {
  display: none;
}

.nav > .nav-links {
  float: right;
  font-size: 18px;
}

.nav > .nav-links > a {
  display: inline-block;
  padding: 10px 30px 13px 30px;
  text-decoration: none;
  color: #ecf1fb;
}
a.login {
  color: #000 !important;
  background-color: #ffffff !important;
  border-radius: 50px;
}
.nav > .nav-links > a:hover {
  color: #333;
}

.nav > #nav-check {
  display: none;
}

/* center div */

.center-div {
  position: absolute;
  top: 30%;
  left: 0;
  text-align: center;
  .main-heading {
    width: calc(150px / 2);
    margin-left: 100px;
    h1 {
      color: #fff;
      font-size: 56px;
    }
  }
}
.fabs {
  bottom: 0;
  position: fixed;
  margin: 1em;
  right: 0;
  z-index: 998;
}
.fab {
  display: block;
  width: 56px;
  height: 56px;
  top: -10px;
  bottom: 0;
  border-radius: 50px 50px 1px 50px;
  text-align: center;
  color: #f0f0f0;
  float: right;
  margin-right: 20px;
  box-shadow: 0 0 4px rgba(0, 0, 0, 0.14), 0 4px 8px rgba(0, 0, 0, 0.28);
  cursor: pointer;
  -webkit-transition: all 0.1s ease-out;
  transition: all 0.1s ease-out;
  position: relative;
  z-index: 998;
  overflow: hidden;
  background: #ffffff;
}

.fab > i {
  font-size: 2em;
  line-height: 55px;
  -webkit-transition: all 0.2s ease-out;
  -webkit-transition: all 0.2s ease-in-out;
  transition: all 0.2s ease-in-out;
}

@media (max-width: 1024px) {
  .nav > .nav-btn {
    display: inline-block;
    position: absolute;
    right: 0px;
    top: 40px;
  }

  .nav > .nav-btn > label {
    display: inline-block;
    width: 50px;
    height: 50px;
    padding: 13px;
  }

  .nav > .nav-btn > label:hover,
  .nav #nav-check:checked ~ .nav-btn > label {
    background-color: rgba(0, 0, 0, 0.3);
  }

  .nav > .nav-btn > label > span {
    display: block;
    width: 25px;
    height: 10px;
    border-top: 2px solid #eee;
  }

  .nav > .nav-links {
    position: absolute;
    display: block;
    width: 100%;
    background-color: #333;
    height: 0px;
    transition: all 0.3s ease-in;
    overflow-y: hidden;
    top: 90px;
    left: 0px;
    z-index: 9999;
  }

  .nav > .nav-links > a {
    display: block;
    width: 100%;
  }

  .nav > #nav-check:not(:checked) ~ .nav-links {
    height: 0px;
  }

  .nav > #nav-check:checked ~ .nav-links {
    height: calc(50vh - 50px);
    overflow-y: auto;
  }
  .center-div {
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    text-align: center;
    .main-heading {
      width: 100%;
      margin: auto;
      h1 {
        font-size: 44px;
      }
    }
  }
}
</style>