<template>
  <div
    class="modal fade"
    id="newsletterModal"
    tabindex="-1"
    role="dialog"
    aria-labelledby="exampleModalLabel"
    aria-hidden="true"
  >
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <button type="button" class="close" data-dismiss="modal" aria-label="Close">
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div>
          <div class="card promoting-card p-2">
            <h3 class="modal-title mb-2" id="exampleModalLabel">
              <b>{{ newsletter_subs_data.title }}</b>
            </h3>
            <img :src="newsletter_subs_data.image" class="rounded-circle m-auto" height="150px" width="150px" alt="avatar" />
            <div class="container form-group mt-3">
              <input type="email" class="form-control" placeholder="Enter your email" />
              <button type="submit" class="btn btn-sponsorship mt-2 btn-block">Subscribe</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: ["newsletter_subs_data"]
};
</script>
<style scoped>
.btn-sponsorship {
  color: #ff5c03 !important;
  padding: 0.6em;
  border: 1px solid;
  border-color: #ff5c03;
  border-radius: 0.25rem;
  font-weight: 800;
}

.btn-sponsorship:hover {
  color: #fff !important;
  background: #ff5c03;
  transition: 0.5s;
}
</style>