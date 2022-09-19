<template>
  <div class="bg-white side-bar">
    <ul class="list-unstyled">
        <li class="rounded">
            <div class="d-flex align-items-center"><img src="https://app.netzeroinsights.com/images/icons/6.Menu_Black.png" alt=""> <span>Menu</span></div>
        </li>
        <li class="rounded">
            <div class="d-flex align-items-center"><img src="https://app.netzeroinsights.com/images/icons/6.Dashboard_Black.png" alt=""> <span>Dashboard</span></div>
        </li>
        <li class="rounded active">
            <div class="d-flex align-items-center"><img src="https://app.netzeroinsights.com/images/icons/6.Organizations_Green.png" alt=""> <span>Organizations</span></div>
        </li>
        <li class="rounded">
            <div class="d-flex align-items-center"><img src="https://app.netzeroinsights.com/images/icons/0.Hearth_Black.png" alt=""> <span>Portfolios</span></div>
        </li>
        <li class="rounded">
            <div class="d-flex align-items-center"><img src="https://app.netzeroinsights.com/images/icons/6.Saved_Black.png" alt=""> <span>Saved searches</span></div>
        </li>
        <li class="rounded">
            <div class="d-flex align-items-center"><img src="https://app.netzeroinsights.com/images/icons/6.Settings_Black.png" alt=""> <span>Settings</span></div>
        </li>
    </ul>
  </div>
</template>

<script>
export default {

}
</script>

<style lang="scss" scoped>
.side-bar{
    display: flex;
    flex-direction: column;
    li{
        padding: 0.625rem;
        margin: 0.625rem 0;
        cursor: pointer;
        img{
            height: 24px;
            width: 24px;
        }
        span{
            margin-left: 00.625rem;
            font-weight: 300;
            display: none;
        }
        &:hover{
            background: #e6f5e9;
        }
        &.active{
            background: #e6f5e9;
            span{
                font-weight: 500;
                color: #7bd08c;
            }
        }
    }
    &:hover{
        span{
            display: initial;
        }
    }
}
</style>