<template>
  <header>
    <div class="col">
      <img class="logo pr-3" src="@/assets/logo.png" alt="" />
    </div>
    <div class="col px-3">
      <div class="form-group mb-0 position-relative">
        <img
          src="https://app.netzeroinsights.com/images/icons/0.Search.png"
          class="icon icon-md"
          style="z-index: 1"
        />
        <div class="position-relative">
          <input
            name="Startup search"
            placeholder="Search climate startups"
            id="header-searchbar"
            title="Startup search"
            autocomplete="off"
            type="text"
            class="form-control"
            style="padding-left: 35px; border-radius: 1rem"
          />
          <!---->
        </div>
      </div>
    </div>
    <div class="col">
        
    </div>
  </header>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
header {
  padding: 15px 50px;
  display: flex;
  display: -ms-flexbox;
  background: #fff;
  -webkit-box-pack: justify !important;
  justify-content: space-between !important;
  flex-direction: row;
}
.logo {
  width: 100px;
}
.form-group {
  .icon {
    left: 0.5rem;
    position: absolute;
    top: 0.375rem;
    height: 1.125rem;
    width: 1.125rem;
  }
  input {
    padding-left: 35px;
    border-radius: 1rem;
    appearance: none;
    background-color: #fff;
    border: 1px solid hsla(0, 0%, 44%, 0.12);
    height: 2rem;
    padding: 0 1rem;
  }
  ::placeholder {
    color: hsla(0, 0%, 44%, 0.3);
    font-weight: 300;
    font-size: 16px;
    opacity: 1; /* Firefox */
  }

  :-ms-input-placeholder {
    color: hsla(0, 0%, 44%, 0.3);
    font-size: 16px;
    font-weight: 300;
  }

  ::-ms-input-placeholder {
    color: hsla(0, 0%, 44%, 0.3);
    font-size: 16px;
    font-weight: 300;
  }
  .form-control {
    color: #232426;
    width: 100%;
  }
}
</style>