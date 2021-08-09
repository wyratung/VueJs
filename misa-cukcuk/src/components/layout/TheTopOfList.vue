<template>
  <div id="topOfList">
      <div class="top-of-list">
        <h1>Danh sách nhân viên</h1>
        <div class="wrapper-btn">
          <div class="button #del-att del-att">Xóa</div>
          <div class="button add-att">
            <div class="add-mems-icon"></div>
            <p>Thêm nhân viên</p>
          </div>
        </div>
      </div>
      <div class="search">
        <div class="search_places">
          <input
            class="search_places__code"
            type="text"
            placeholder="Tìm kiếm theo Mã, Tên hoặc Số Điện Thoại"
          />
          <div class="search_places__department">
            <div class="dropdown">
              <div class="dropdown-header-wrapper">
                <span class="dropdown-value dropdown-value-1"></span>
                <i class="fas fa-chevron-down icon-down show"></i>
                <i class="fas fa-chevron-up icon-up"></i>
              </div>
              <ul class="dropdown-list dropdown-list-1"></ul>
            </div>
          </div>
          <div class="search_places__position">
            <div class="dropdown">
              <div class="dropdown-header-wrapper">
                <span class="dropdown-value dropdown-value-2"></span>
                <i class="fas fa-chevron-down icon-down show"></i>
                <i class="fas fa-chevron-up icon-up"></i>
              </div>
              <ul class="dropdown-list dropdown-list-2"></ul>
            </div>
          </div>
        </div>
        <div class="refresh" id="refresh">
          <div class="refresh-icon"></div>
        </div>
      </div>
  </div>
</template>

<script>

export default {

}
</script>

<style>

</style>